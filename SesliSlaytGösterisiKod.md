# Gorsel-Programlama-II-Hafta-2
Hafta 2
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Media;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace SlaytGösterisiSesli
{
    public partial class Form1 : Form
    {// formun üyeleri
        int sayac;
        SoundPlayer sndplyr = new SoundPlayer(ResourceSesler.chimes);

        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            sayac = 0;
            timer1.Start();
            pictureBox1.Image = ResourceGörüntüler.anakart;
            pictureBox1.SizeMode = PictureBoxSizeMode.Zoom;
            sndplyr.Load();
            sndplyr.Play();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            timer1.Interval=(2000);// Hızını belirlersiniz 2000milisaniye/2Saniye
            sayac++;
            int i = sayac % 8;
            switch (i)
            {
                case 0:
                    pictureBox1.Image = ResourceGörüntüler.ddr4;
                    sndplyr.Stream = ResourceSesler.chord;
                    sndplyr.Load(); sndplyr.Play();
                        break;
                case 1:
                    pictureBox1.Image = ResourceGörüntüler.geforce_rtx_3090;
                    sndplyr.Stream = ResourceSesler.ding;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 2:
                    pictureBox1.Image = ResourceGörüntüler.islemci;
                    sndplyr.Stream = ResourceSesler.ir_inter;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 3:
                    pictureBox1.Image = ResourceGörüntüler.kasa;
                    sndplyr.Stream = ResourceSesler.notify;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 4:
                    pictureBox1.Image = ResourceGörüntüler.klavye;
                    sndplyr.Stream = ResourceSesler.recycle;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 5:
                    pictureBox1.Image = ResourceGörüntüler.mouse;
                    sndplyr.Stream = ResourceSesler.ringout;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 6:
                    pictureBox1.Image = ResourceGörüntüler.yok;
                    sndplyr.Stream = ResourceSesler.tada;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                case 7:
                    pictureBox1.Image = ResourceGörüntüler.anakart;
                    sndplyr.Stream = ResourceSesler.chimes;
                    sndplyr.Load(); sndplyr.Play();
                    break;
                default: MessageBox.Show("Switch Default düştü");
                    break;
            }
        }
    }
}
