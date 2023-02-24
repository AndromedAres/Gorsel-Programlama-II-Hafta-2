# Gorsel-Programlama-II-Hafta-2
Hafta 2
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
/* // datarow /verisatırı : Satırlar alt alta gelerek tabloyu oluştururlar
            DataTable dt = new DataTable();
            // içinde birden fazla dataTable barındıran yapıya da dataSet denir
            DataSet ds = new DataSet(); */ //set küme anlamına gelir

namespace VeriSatiriTablosuKumesi
{
    public partial class Form1 : Form
    {//forma üye olaak data set yapalım ve çeşitli metodlarda yapılan datatableları bunun içine koyalım
        //böylelikle herhangi bir metottan tüm datatablelara erişelebilir olsun
        DataSet ds = new DataSet(); // form1 üyesi olarak ds
        public Form1()
        {
            InitializeComponent();
        }

        private void button4_Click(object sender, EventArgs e)
        {//Kişiler dataTable Xml den oku
            //datagridde gösterelim
            DataTable dt = new DataTable();
            dt.ReadXmlSchema("kisilerschema.xml");
            dt.ReadXml("kisiler.xml");
            //datatableı datasete aktaralım
            ds.Tables.Add(dt);
            //kullanıcı isterse button2 de gridden göstersin

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {//kişiler datatable oluşturalım
            DataTable KisilerDt = new DataTable("Kişiler");
            KisilerDt.Clear(); // verileri temizle
            //Tablonun kolon adlarını ve veri tiplerini bildirelim
            KisilerDt.Columns.Add("KişiNo", typeof(int));
            KisilerDt.Columns.Add("AdSoyad", typeof(string));
            KisilerDt.Columns.Add("Telefon", typeof(string));
            DataRow row = KisilerDt.NewRow();
            row["KişiNo"] = 1;//0. hücre
            row["AdSoyad"] = "Faruk Tabutçuoğulları"; //1.hücre row[1] ="Faruk Tabutçuoğulları"
            row["Telefon"] = "05537394245"; //2. hücre row[2]="..."
            row["Gelir"] = 3456.7;
            //satırı tabloya ekleyelim
            KisilerDt.Rows.Add(row);
            //Bir satır daha
            DataRow row2 = KisilerDt.NewRow();
            row2["KişiNo"] = 2;//0. hücre
            row2["AdSoyad"] = "Eyüp Sabri";//1.hücre 
            row2["Telefon"] = "05537394246"; //2. hücre 
            row2["Gelir"] = 3056.7;
            KisilerDt.Rows.Add(row2);
            //bir satır daha
            DataRow row3 = KisilerDt.NewRow();
            row3["KişiNo"] = 3;//0. hücre
            row3["AdSoyad"] = "Mithat Bayındıraşağı";//1.hücre 
            row3["Telefon"] = "05537394236"; //2. hücre 
            row3["Gelir"] = 2056.7;
            KisilerDt.Rows.Add(row3);
            //datagridviewda göster
            dataGridView1.DataSource = KisilerDt;
            //datatable ı formun dataseti içine koyalım
            //Yoksa yerleştir
            if(!ds.Tables.Contains("Kişiler"))
            ds.Tables.Add(KisilerDt);
            

        }

        private void button2_Click(object sender, EventArgs e)
        {//Kişiler datagridde göster
            dataGridView1.DataSource = ds.Tables["Kişiler"] ; // KisilerDt

        }

        private void button3_Click(object sender, EventArgs e)
        {//Kişiler DataTabel XML Dosyasına kaydet
            if (ds.Tables.Contains("Kişiler"))
            {//varsa ds içindeki kişiler tablosuna alalım
                DataTable kisiler = ds.Tables["Kişiler"];
                //datasını xml kaydet
                kisiler.WriteXml("kisiler.xml");
                //şeması(datalar hakkında bilgi) da olmak zorunda
                kisiler.WriteXmlSchema("kisilerschema");

            }



        }
    }
}
