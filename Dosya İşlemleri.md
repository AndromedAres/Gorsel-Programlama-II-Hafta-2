# Gorsel-Programlama-II
Hafta 2
namespace Dosya_İşlemler_Görsel_Programalama2_Hafta_2
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button3_Click(object sender, EventArgs e)
        {//folder BrowserDialog kullanarak
            //dosyalar için dizin yeri ya da yolu belirle textbx2 ye yaz
            string dosyaYolu;
            //FolderBrowser açmak için başlangıç dizini kullanıcının belgelerim dizini olsun
            string belgeler = Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);
            folderBrowserDialog1.SelectedPath = belgeler;
            folderBrowserDialog1.Description = "Dizin Seçiniz";
            DialogResult dr = folderBrowserDialog1.ShowDialog();
            if (dr == DialogResult.OK)
            {//Eğer kullanıcı Ok dediyse seçilen dizini klasörün dosya yolu ddeğişkenine ata 
                dosyaYolu = folderBrowserDialog1.SelectedPath;
                textBox2.Text = dosyaYolu;
            }

        }

        private void button1_Click(object sender, EventArgs e)
        {
            //dizini txtbx 2 den openfiledialog ile açıp okunmak istenen dosyayı seçelim,okuyup txtbx1 de gösterelim
            openFileDialog1.Title = "Tex Dosyası Aç";
            openFileDialog1.Filter = "Text Dosyası|.txt|Csharp|.cs|VisualBasic|*.vb";
            openFileDialog1.InitialDirectory = textBox2.Text;//başlangıç dizini
            openFileDialog1.FileName = textBox3.Text;//dosya adı
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {//eğer diyalog sonucu ok ise dosyayı aç oku 
                string dosyaYoluAd = openFileDialog1.FileName;
                //dosyayı satır satır okuyup,yazi değişkeninde toplamsal olarak biriktirelim
                string yazi = "";
                string satir;
                StreamReader sr = new StreamReader(dosyaYoluAd);
                satir = sr.ReadLine();
                while (satir != null)
                {
                    yazi = yazi + satir + Environment.NewLine;
                    satir = sr.ReadLine();
                }
                textBox1.Text = yazi;//yazi da biriktirilen dosya içeriğini txtbx1 e aktardık 
                sr.Close();
                textBox2.Text = dosyaYoluAd;//değişmiş olabilir güncelle
                 }
            }

        private void button2_Click(object sender, EventArgs e)
        {//txtbx2de dizine açıp, dizini ve dosya adını belirleyip txtbx1 de yazılanları kaydedelim
            saveFileDialog1.Title = "Text Dosyasını Kaydet";
            saveFileDialog1.Filter = "Text Dosyası|*.txt|Csharp|*.cs|VisualBasic|*.vb";
            saveFileDialog1.InitialDirectory = textBox2.Text; //Başlangıç dizini
            saveFileDialog1.FileName = textBox3.Text;
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {//savefile diyalog kullanıcı ile etkinleşti sonucu olumlu ise :
                //kullanıcının seçtiği dosya yolunu ve adını alalım
                string dosyaYolAd = saveFileDialog1.FileName;
                bool apent = true; //chckbx koy ordan al bu değeri
                //Akıç yazıcısı, dosya yoksa yaratır kaydedir,
                //dosya varsa APPEND = False üzerine yazar,
                //dosya varsa APPEND = True ise dosyanın sonuna yazar.
                StreamWriter sw = new StreamWriter(dosyaYolAd, apent);
                sw.WriteLine(textBox1.Text);
                sw.Close();
                textBox2.Text = dosyaYolAd; //son duruma göre güncelleme

                

            }

        }
    }
}
