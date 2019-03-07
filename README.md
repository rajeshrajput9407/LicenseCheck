# LicenseCheck
you can use LicenseCheck code 
////////////////////////////////////****************************************************/////////////////////////////////////////////

static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            //Application.Run(new Form1());
            //Application.Run(new CheckLilcence());
            string filePath = new DirectoryInfo(Environment.CurrentDirectory).Parent.Parent.FullName;
            var fullPath = Path.Combine(filePath, @"License\licenseFile.txt");
            //DirectoryInfo dinfo = new DirectoryInfo(fullPath);
            //FileInfo[] smFiles = dinfo.GetFiles("licenseFile.txt");

            if (File.Exists(fullPath))
            {
                string[] lines = System.IO.File.ReadAllLines(fullPath);
                if(Licence.CheckProduct(lines[0].Trim(), lines[1].Trim()))
                {
                    Application.Run(new Form2());
                }
                else
                {
                    MessageBox.Show("Some error occure,Please contact Administrator", "License Error", MessageBoxButtons.OK, MessageBoxIcon.Information);

                    Application.Run(new CheckLilcence());

                }
            }
            else
            {
                Application.Run(new CheckLilcence());

            }
            
           
        }
        
        ////////////////////////////////////////****************************************//////////////////////////////////////
        private void btnSubmit_Click(object sender, EventArgs e)
        {
            if (string.IsNullOrEmpty(txtProductName.Text.Trim()))
            {
                label4.Text = "*";
                return;
            }
            if (string.IsNullOrEmpty(txtProductKey.Text.Trim()))
            {
                label5.Text = "*";
                return;
            }
            string filePath = new DirectoryInfo(Environment.CurrentDirectory).Parent.Parent.FullName;
            var fullPath = Path.Combine(filePath, @"License\licenseFile.txt");
            if (File.Exists(fullPath))
            {
                File.Delete(fullPath);
                //using (var fs = new FileStream(fullPath, FileMode.Truncate))
                //{
                //}
            }
             
                TextWriter tw = new StreamWriter(fullPath);
                tw.WriteLine(txtProductName.Text.Trim());
                tw.WriteLine(txtProductKey.Text.Trim());
                tw.Close();

                string[] lines = System.IO.File.ReadAllLines(fullPath);
                if (Licence.CheckProduct(lines[0].Trim(), lines[1].Trim()))
                {
               
                Form2 form2 = new Form2();
                form2.Show();
                this.Hide();
                 //Application.Run(new Form2());
                }
                else
                {
                MessageBox.Show("Please enter valid license credentials", "License Error", MessageBoxButtons.OK, MessageBoxIcon.Error);
                //Application.Run(new CheckLilcence());
            }

        }
