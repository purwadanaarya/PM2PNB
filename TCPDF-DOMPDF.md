##################################TCPDF##############################################
1. Download library http://sourceforge.net/projects/tcpdf/files/ ATAU https://github.com/tecnickcom/TCPDF/archive/refs/heads/main.zip
3. Ekstrak semua file dan taruh di folder libraries, /application/libraries/tcpdf
4. Buat sebuah file /application/libraries/Pdf.php

<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');

require_once dirname(__FILE__) . '/tcpdf/tcpdf.php';

class Pdf extends TCPDF
{
    function __construct()
    {
        parent::__construct();
    }
}

/* End of file Pdf.php */
/* Location: ./application/libraries/Pdf.php */

4. Gunakan library $this->load->library('Pdf');
5. Penggunaan :

<?php
    $pdf = new Pdf('P', 'mm', 'A4', true, 'UTF-8', false);
    $pdf->SetTitle('Laporan');
    $pdf->SetTopMargin(20);
    $pdf->setFooterMargin(20);
    $pdf->SetAutoPageBreak(true);
    $pdf->SetAuthor('Author');
    $pdf->SetDisplayMode('real', 'default');
    $pdf->AddPage();
    $pdf->Write(5, 'Contoh Penggunaan TCPDF');
    $pdf->Output('contohlaporan.pdf', 'I');
?>

####################################DOMPDF##############################################
1. Edit file config $config['composer_autoload'] = FALSE
2. Download DOMPDF https://github.com/dompdf/dompdf/releases
3. Ekstrak semua file dan taruh di folder libraries, /application/libraries/tcpdf
4. Buat sebuah file /application/libraries/Pdfgenerator.php

<?php defined('BASEPATH') or exit('No direct script access allowed');
require_once 'dompdf-master/autoload.inc.php';
use Dompdf\Dompdf;
use Dompdf\Options;

class Pdfgenerator
{
    public function generate($html, $filename = '',  $paper = '', $orientation = '', $stream = TRUE)
    {
        $options = new Options();
        $options->set('isRemoteEnabled', TRUE);
        $dompdf = new Dompdf($options);
        $dompdf->loadHtml($html);
        $dompdf->setPaper($paper, $orientation);
        $dompdf->render();
        if ($stream) {
            $dompdf->stream($filename . ".pdf", array("Attachment" => 0));
            exit();
        } else {
            return $dompdf->output();
        }
    }
}

5. Penggunaan

$this->load->library('pdfgenerator');

$file_pdf = 'Judul';
$paper = 'A4';
$orientation = "landscape";
$html = $this->load->view('laporan', $data);
$this->pdfgenerator->generate($html, $file_pdf, $paper, $orientation);

////////ATAU

$this->pdfgenerator->generate($html, 'Judul', 'A4', "landscape");
