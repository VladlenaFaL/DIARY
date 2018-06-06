using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Xml.Serialization;
using System.IO;

namespace kursova
{
    public partial class Form2 : Form
    {
        public class Podiya
        {
            public string naz;
            public string typ;
            public string data;
            public string chas;
            public string opys;
            public Podiya()
            {
                naz = "";
                typ = "";
                data = "";
                chas = "";
                opys = "";
            }
            public Podiya(string naz, string typ, string data, string chas, string opys)
            {
                this.naz = naz;
                this.typ = typ;
                this.data = data;
                this.chas = chas;
                this.opys = opys;
            }
        }

        class PodiyaList
        {
            XmlSerializer sr = new XmlSerializer(typeof(List<Podiya>));
            public List<Podiya> Shodennyk = new List<Podiya>();
            public void Reading()
            {
                FileStream file = new FileStream("data.txt", FileMode.Open, FileAccess.Read, FileShare.None);
                Shodennyk = (List<Podiya>)sr.Deserialize(file);
                file.Close();
            }
        }

        PodiyaList A = new PodiyaList();

        public Form2(string tofind)
        {
            InitializeComponent();
            A.Reading();
            int temp = 0;
            for (int i = 0; i < A.Shodennyk.Count; i++)
                if (A.Shodennyk[i].naz == tofind)
                {
                    temp = i;
                    break;
                }
            richTextBox1.Text = A.Shodennyk[temp].opys;
        }
    }
}
