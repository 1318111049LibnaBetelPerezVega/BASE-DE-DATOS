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

namespace jaisbe1
{
    public partial class jaisbe : Form
    {
        public jaisbe()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            string connection = "datasource=localhost;port=3306;username=root;password=;database=jaisbe";
            string query = "SELECT * FROM jaisbe";
            MySqlConnection conectionDatabase = new MySqlConnection(connection);
            MySqlCommand databaseCommand = new MySqlCommand(query, conectionDatabase);
            databaseCommand.CommandTimeout = 60;
            MySqlDataReader reader;

            try
            {
                conectionDatabase.Open();
                reader = databaseCommand.ExecuteReader();
                if (reader.HasRows)
                {
                    while (reader.Read())
                    {
                        //Console.WriteLine(reader.GetString(0) + " " + reader.GetString(1) + " " + reader.GetString(2) + " "+reader.GetString(3));
                        string[] row = { reader.GetString(0), reader.GetString(1), reader.GetString(2), reader.GetString(3) };
                        var listViewItem = new ListViewItem(row);
                        listView1.Items.Add(listViewItem);
                    }
                }
                else
                {
                    Console.WriteLine("No se encontraron datos");
                }
                conectionDatabase.Close();
            }
            catch (Exception ex)
            { 
                MessageBox.Show(ex.Message);
            }  

        }
        private void GuardarUsuario()
        {
            string connection = "datasource=localhost; port=3306;username=root;password=;database=jaisbe";
            string query = "SELECT * FROM jaisbe";
            MySqlConnection conectionDatabase = new MySqlConnection(connection);
            MySqlCommand databaseCommand = new MySqlCommand(query, conectionDatabase);
            databaseCommand.CommandTimeout = 60;
            MySqlDataReader reader;
            try
            {
                conectionDatabase.Open();
                reader = databaseCommand.ExecuteReader();
                if(reader.HasRows)
                {
                   while (reader.Read())
                    {
                        //Console.WriteLine(reader.GetString(0) + " " + reader.GetString(1) + " " + reader.GetString(2) + " "+reader.GetString(3));
                        string[] row = { reader.GetString(0), reader.GetString(1), reader.GetString(2), reader.GetString(3) };
                        var listViewItem = new ListViewItem(row);
                        listView1.Items.Add(listViewItem);
                    }
                }
                else
                {
                    Console.WriteLine("No hay ningun dato");
                }
                conectionDatabase.Close();
            }
            catch(Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void BorrarUsuario()
        {
            string connection = "datasource=localhost;port=3306;username=root;password=;database=jaisbe";
            string query = "DELETE FROM jaisbe WHERE id='" + textBox5.Text + "' ";
            MySqlConnection conectionDatabase = new MySqlConnection(connection);
            MySqlCommand databaseCommand = new MySqlCommand(query, conectionDatabase);
            databaseCommand.CommandTimeout = 60;

            try
            {
                conectionDatabase.Open();
                MySqlDataReader reader1 = databaseCommand.ExecuteReader();
                MessageBox.Show("Lograste borrar el dato ");
                conectionDatabase.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }

        private void Modificar()
        {
            string connection = "datasource=localhost;port=3306;username=root;password=;database=jaisbe";
            string query = "UPDATE jaisbe SET nombre='" + textBox1.Text + "',apellido_paterno='" + textBox2.Text + "',apellido_materno='" + textBox3.Text + "',direccion='" + textBox4.Text + "'  id='" + textBox5.Text + "' ";
            MySqlConnection conectionDatabase = new MySqlConnection(connection);
            MySqlCommand databaseCommand = new MySqlCommand(query, conectionDatabase);
            databaseCommand.CommandTimeout = 60;

            try
            {
                conectionDatabase.Open();
                MySqlDataReader reader1 = databaseCommand.ExecuteReader();
                MessageBox.Show("Lograste Modificar el dato, eres un Crack");
                conectionDatabase.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }

        }
        private void BuscarUsuario()
        {
            string Connect = "datasource=localhost;port=3306;username=root;password=;database=jaisbe;";
            string query = "SELECT * FROM jaisbe where id='" + textBox5.Text + "' ";
            MySqlConnection databaseConnection = new MySqlConnection(Connect);
            MySqlCommand commandDatabase = new MySqlCommand(query, databaseConnection);
            commandDatabase.CommandTimeout = 60;
            MySqlDataReader reader;


            try
            {
                databaseConnection.Open();
                reader = commandDatabase.ExecuteReader();
                if (reader.HasRows)
                {
                    listView1.Items.Clear();
                    while (reader.Read())
                    {
                        string[] row = { reader.GetString(0), reader.GetString(1), reader.GetString(2), reader.GetString(3) };
                        // var ListViewItems = new ListViewItem(row);
                        textBox1.Text = row[1];
                        textBox2.Text = row[2];
                        textBox3.Text = row[3];
                    }
                }
                else
                {
                    Console.WriteLine("No se encontro nada");
                }
                databaseConnection.Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }

        }

        private void MostrarUsuario()
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {
            string Connect = "datasource=localhost;port=3306;username=root;password=;database=jaisbe;";
            string query = "SELECT * FROM jaisbe";
            MySqlCommand mySqlCommand = new MySqlCommand(query, new MySqlConnection(Connect));
            mySqlCommand.CommandTimeout = 60;
            MySqlDataReader reader;
            
            try
            {
                new MySqlConnection(Connect).Open();
                reader = mySqlCommand.ExecuteReader();
                if (reader.HasRows)
                {
                    listView1.Items.Clear();
                    while (reader.Read())
                    {
                        string[] row = { reader.GetString(0), reader.GetString(1), reader.GetString(2), reader.GetString(3) };
                        var ListViewItems = new ListViewItem(row);
                        listView1.Items.Add(ListViewItems);
                    }
                }
                else
                {
                    Console.WriteLine("No se encontro nada");
                }
                new MySqlConnection(Connect).Close();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
        }
        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void listView1_SelectedIndexChanged(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, EventArgs e)
        {// Guardar Dato
            if (textBox1.Text == "")
            {
                MessageBox.Show("Te falto nombre");
            }
            else if (textBox2.Text == "")
            {
                MessageBox.Show("Te falto direccion");
            }
            else if (textBox3.Text == "")
            {
                MessageBox.Show("Te falto poner apellido");
            }
            else
            {

                GuardarUsuario();
                MostrarUsuario();
                BuscarUsuario();
                BorrarUsuario();
                Modificar();
                textBox1.Text = "";
                textBox2.Text = "";
                textBox3.Text = "";

            }
        }

        private void button10_Click(object sender, EventArgs e)
        {//Actualizar
            MostrarUsuario();
        }
        private void button6_Click(object sender, EventArgs e)
        {//buscar
            BuscarUsuario();
        }
        private void button8_Click(object sender, EventArgs e)
        {//modificar
            Modificar();
        }
        private void TextBox9_TextChanged(object sender, EventArgs e)
        {
            GuardarUsuario();
        }

        private void textBox8_TextChanged(object sender, EventArgs e)
        {

        }

        private void textBox10_TextChanged(object sender, EventArgs e)
        {

        }

        private void button7_Click(object sender, EventArgs e)
        {
            BorrarUsuario();
        }
    }
}
