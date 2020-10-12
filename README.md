# BASE-DE-DATOS
BASE DE DATOS, tabla que muestra los nobres, direccion y apaellido con solo poner un ID, te permite eliminar a usuarios también puedes buscar usuarios y agregar usuarios nuevos.
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using MySql.Data.MySqlClient;

namespace BaseDeDatosjaisbe
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string connection = "datasource=locahost=3306;username=root;pasword";
            string query = "SELECT * FROM jaisbe";
            MySqlConnection conectionDatabase = new MySqlConnection; conectionDatabase(connection);
            MySqlCommand databaseCommand = new MySqlCommand(query, conectionDatabase);
            databaseCommand.CommandTimeout = 60;
            MySqlDataReader reader;

            try
            {
                conectionDatabase.Open();
                reader = databaseCommand.ExecuteReader();
                if (reader.HasRows())
                {
                    Console.WriteLine(reader.GetString(0) + " " + reader.GetString(1) + " " + reader.GetString(2) + " " + reader.GetString(3) + " " + reader.GetString(4) + " " + reader.GetString(5));

                }
            }
            else
            {
                Console.WriteLine("No se encontraron los datos");
            }
            conectionDatabase.Close();

        }
        catch (Exeption ex)
            {
            MessageBox.Show(alerta.Message);
           }
           
       }
    }
}
