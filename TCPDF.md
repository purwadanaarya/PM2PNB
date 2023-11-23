1. Download library http://sourceforge.net/projects/tcpdf/files/
2. Ekstrak semua file dan taruh di folder libraries, /application/libraries/tcpdf
3. Buat sebuah file /application/libraries/Pdf.php

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

