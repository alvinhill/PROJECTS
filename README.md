
![ATM](https://github.com/alvinhill/PROJECTS/assets/132315899/bfcc84d9-b951-4fd1-9ac1-84da5267e742)
# ATM Program

This program simulates an atm program.  It checks the pin code and gives you the option for withdrawal, deposits or see the statement.
This interface is linked to an SQL database.  It has two tables.  One is a customer table and the other is a transaction table.  The customer table has a primary key that links to each transaction made by each customer.
We can look at the statement.  This shows the related information is transaction order.  It also gives a running total and final balance.  
We can withdraw and/or look at other accounts.
It has an admin panel that can be used to do different queries.  
This program has three classes.  
It has an “action” class used to supply values for the selected tasks to perform.
It has a “main” class to provide the main interface and give numeric values and sound to the buttons.
It has a “result” class that is under construction.
It has a “state” statement class to show the account in the database.
It has a data1 class that 

1.)	Does the math for deposits and withdrawals.
2.)	 Connects to the data base.   
3.)	It stores the pin codes and the comparison method to control secure access.

It has a test class which is inactive now.
The upgrade path for this is:

See the video at my portfolio site:  http://alvinrainhill.com/EXP-X3.html

1.)	Upgrade the admin panel
2.)	Create other built-in queries to generate reports and totals for the admin panel.
3.)	Code a “Create New Account” for new customers.
4.)	Finish or delete the “results” and “test” classes.

# Code Example

# ATM CODE
## This class does several things.

1.)	It validates the pin code.
2.)	Supplies the transaction label.
3.)	Does the transaction math.
4.)	Opens the database and inputs the value into the database.

 class DATA1
    {
        private decimal balance ;

        private string pin;
        public decimal money;
        public string VCODE;
        public bool status= false ;
        // static public string INPUT { get; set; } = "7111";
        static public string INPUT;
        //= "7111";
        public string[] match = new string[10] { "9111", "7111", "8111", "4111", "5111", "6111", "3111", "2111", "1111", "1001"};// 10
      //public string[] match = new string[10] { "9111", "7111", "8111", "4111", "5111", "6111", "3111", "2111", "1111", "1001" };// 10

        public decimal BALANCE
        {
            get
            {
                return balance ;
            }
            set
            {
                balance  = value;
            }
        }
        public string PIN
        {
            get
            {
                return pin;
            }
            set
            {
                pin = value;
                for (int i = 0; i < match.Length ; i++)
                {
                    if (pin == match[i])
                    {
                        INPUT = pin;
                        status = true;
                      //  System.Windows.Forms.MessageBox.Show("GOOD");
                        break;
                    }
                    else if (i ==9)//9
                    {
                        System.Windows.Forms.MessageBox.Show("BAD PIN");
                    }
                }
            }
        }
           public decimal MONEY
            {
            get
            {
                return money;
            }
            set
            {
                money = value;
            }
            }
        // DEPOSIT METHOD
        public decimal DEPOSIT()
        {
             balance = balance + money;
         if (money > 0)
           {
                VCODE = "DEPOSIT";
                RECORD();
          }
            return balance;
        }
        // WITHDRAWAL METHOD
        public decimal WITHDRAW()
        {
            balance = balance - money;
            if (balance < 0)
            {
                VCODE = "WITHDRAWAL";
                RECORD();
            }
            return balance;
        }
        public void RECORD()
        {
            // THIS WORKS TO PUT A VARIABLE INTO THE DATABASE !!!
            SqlConnection SQLCONNECT = new SqlConnection(@"Data Source = SATURN; Initial Catalog = NEWBANK; Integrated Security = true");
            SqlCommand SQLCMD = new SqlCommand("select * from ACCOUNTS2 WHERE PIN ='"+INPUT +"'", SQLCONNECT);
            SQLCONNECT.Open();
            SqlDataReader SQLREADER = SQLCMD.ExecuteReader();
            SQLREADER.Read();
            string DPIN;
            string DACCTNUMBER;
            DPIN = SQLREADER.GetValue(1).ToString();
            DACCTNUMBER = SQLREADER.GetValue(2).ToString();
            SQLCONNECT.Close();
            SQLCONNECT.Open();
            // ENTER DATA INTO DATABASE
           var NEWENTRY = "Insert into ACCOUNTS2(PIN,AcctNumber,TransData,CODE) values('" + DPIN + "','" + DACCTNUMBER + "'," + balance  + ", '" + VCODE + "')";// GOOD
            SQLCMD = new SqlCommand(Convert.ToString(NEWENTRY), SQLCONNECT);
            SQLCMD.ExecuteNonQuery();
            SQLCMD.Dispose();
            SQLCONNECT.Close();
        }
    }

![BANK-REC](https://github.com/alvinhill/PROJECTS/assets/132315899/814e0d3d-b9f4-4c7c-bc8b-ed44a5e3854a)


# BANK RECONCILIATION PROGRAM


I always had trouble reconciling my bank account.  (yes, I still write checks.)

It would take me about an hour if everything went right.

I always had trouble doing my bank recs and I would often give up and just take the bank’s balance.  

My checkbook and my statement looked completely different even though it was the same information.

It was a confusing mess for me.

I decided to see if I could write the program.  It would be my first program.  I was able to do it and I use it every month to check my bank account.   

I used a file requestor to load the bank statement file.

My statement would have all the transactions mixed together out of order with confusing labels.  

When I press the “START” button, the magic happens.

All of the checks are at the top of the screen and they are in order.  
Gets rid of the confusing descriptions.
It closely or exactly matches my checkbook.
I use this program every month to do my bank recs in about 25ms instead of the hour that it used to take.  

See my video at my portfolio site:  http://alvinrainhill.com/EXP-X2.html

The upgrade path for this is:
1.)	Make it web based.
2.)	Import other file formats.
3.)	Export the working file to and SQL database to allow advanced data manipulation.
## Code not available at this time due to possible commercial interest. 

# GUITAR STORE
![GUITAR-STORE](https://github.com/alvinhill/PROJECTS/assets/132315899/474ef0b7-57c2-4ec5-8b12-29d773600dd9)

This program allows me to select a guitar to order.  I can select the Brand, Model, Finish and Neck.  
As you can see, the selections are linked to a cost of each item selected.  Each time a new item is selected, to cost and the subtotal is refreshed.   An item code is generated based on each selection.  
After selecting a guitar, we use the cart system in the program.
The cart has the subtotal.  From here select a tax schedule and a shipping zone.
The customer and payment data is entered.  
Note there is error checking in this section.
When ready press “Place Order”
This information is saved in a text file that has a unique sequential number.
Show Text File.
This program has three classes.  
A business class for the guitar section part.  
A cart class for the order information 
and a Datafile class for saving the order information.
See the video of my program at: http://alvinrainhill.com/EXP-X4.html

The upgrade path for this is:
1.)	To be a web-based program with pictures of all the pretty guitars.  
2.)	Save the data to an SQL database and construct queries.

## Code for the guitar store cart.

 class BUSINESS
    {
        private string name;
        private string phone;
        private string address;
        private string email;
        private string creditcard;
        private string expm;
        private string expy;
        private string brand;
        private string model;
        private string color;
        private string neck;
        private string total;
        private string itemcode;
       public static string ERRORCODE="";
        public static int ECN;
      
        public BUSINESS ()
        { }
   
        public string NAME
        {
            get
            {
                  return name;
            }
            set
            {
                // SET NAME TO UPPERCASE
                // CHECK FOR EMPTY FIELD
                name = value.ToUpper() ;

                if (name == "")
                {
                    ERRORCODE = "INCORRECT NAME ENTRY";
                    ECN = 1;
                    DATAFILE.SHOWCODE();
                   // System.Windows.Forms.MessageBox.Show("BAD");
                }
              }
        }
        public string PHONE
        {
            get
            {
                return phone;
            }
            set
            {
                 phone = value;
                // CHECK FOR 10 DIGITS
                // CHECK FOR ALL NUMERIC DATA
               // if (e.KeyChar >='0' && e.KeyChar<='9')
                if (phone.Length <10)
                {
                    ERRORCODE = "INCORRECT PHONE ENTRY";
                    ECN = 1;
                    DATAFILE.SHOWCODE();
                }
            }
        }
        public string ADDRESS
        {
            get
            {
                // CHECK FOR EMPTY FIELD
                return address ;
            }
            set
            {
                // CHECK FOR EMPTY FIELD
                address = value;
                if (address == "")
                {
                    ERRORCODE = "INCORRECT ADDRESS ENTRY";
                    ECN++;
                }
            }
        }
        public string EMAIL
        {
            get
            {
                return email;
            }
            set
            {
                email = value;
                if (email.Contains("@"))
                {
                    email = value;
                }
                else
                {
                    ERRORCODE = "INCORRECT EMAIL ENTRY";
                    ECN++;
                }
            }
        }
        public string CREDITCARD
        {
            get
            {
                return creditcard ;
            }
            set
            {
                creditcard  = value;
                // check for 16 digits
                // check for non numeric data
                if (creditcard.Length < 16)
                {
                    ERRORCODE = "INCORRECT CREDIT CARD ENTRY";
                    ECN = 1;
                    DATAFILE.SHOWCODE();
                }
            }
        }

        //____________________________
        public string EXPM
        {
            get
            {
                return expm;
            }
            set
            {
                expm = value;
                if (expm == "Exp Month")
                {
                    ERRORCODE = "MISSING EPX MONTH ENTRY";
                    ECN++;
                    // CHECK FOR EMPTY FIELD
                }
            }
        }
        //____________________________

        public string EXPY
        {
            get
            {
                return expy;
            }
            set
            {
                // CHECK FOR EMPTY FIELD
                expy = value;
                if (expy == "Exp Year")
                {
                    ERRORCODE = "MISSING EPX YEAR ENTRY";
                    ECN++;
                    // CHECK FOR EMPTY FIELD
                }
            }
        }
        //____________________________
        public string BRAND
        {
            get
            {
                return brand;
            }
            set
            {
                brand = value;
            }
        }
        //____________________________
        public string MODEL
        {
            get
            {
                return model;
            }
            set
            {
                model = value;
            }
        }
        //____________________________
        public string COLOR
        {
            get
            {
                return color;
            }
            set
            {
                color = value;
            }
        }
        //____________________________
        public string NECK
        {
            get
            {
                return neck;
            }
            set
            {
                neck = value;
            }
        }
        //____________________________
        public string TOTAL
        {
            get
            {
                return total;
            }
            set
            {
                total = value;
            }
        }
        //____________________________
        public string ITEMCODE
        {
            get
            {
                return itemcode;
            }
            set
            {
                itemcode = value;
            }
        }
     }

# Sstatistic program.  

![STATISTIC-PROGRAM](https://github.com/alvinhill/PROJECTS/assets/132315899/8b11025d-0f13-42c5-8d2d-d4918df90972)


I wrote this program to demonstrate three different chart types with the same values.  The first is of course a pie graph.  The second is a bar graph and the third is a line graph. 

The pie graph is displayed with colors corresponding to the month label on the right of the window.
The bar graph is self-explanatory.
The line graph displays line uptrends in black and downtrends in red.
I can load a file to input the yearly values.  I can also save them.  
I can enter them manually and display them.  
See the video on my portfolio site at: http://alvinrainhill.com/EXP-X6.html
The upgrade path for this is:
1.)	 Make the interface more user friendly.
2.)	Maybe send the data to an SQL database to allow yearly statistical information to be analyzed.

## Stat Program Code
public partial class Form1 : Form
    {
        //  EVERY THING WORKS
        //  JUST NEED TO LET PIE GRAPH RUN AUTOMATICALLY
        //  NEED LABLES SET UP ON FORM
        
        public Form1()
        {
            InitializeComponent();
        }
          public string Filename { get; private set; }
        private void Set_background(Object sender, PaintEventArgs e)
        {
            Graphics graphics = e.Graphics;
            // SET THE GRAPHICS TO BE THE SAME SIZE OF THE FORM
            Rectangle gradient_rectangle = new Rectangle(0, 0, Width, Height);
            // HORIZONTAL 
            Brush HB = new HatchBrush(HatchStyle.DiagonalBrick, Color.Coral , Color.Gold);
            //APPLY HATCH BRUSH        
            graphics.FillRectangle(HB, 0, 0, Width, Height);
        }
        private void Start_Click(object sender, EventArgs e)
        {
            // SUPPLY TEXT BOX VALUES FOR ALL GRAPHS
            float[] sweepA = new float[12];
            string BOX0; string BOX1; string BOX2; string BOX3;
            string BOX4; string BOX5; string BOX6; string BOX7;
            string BOX8; string BOX9; string BOX10; string BOX11;
            BOX0 = textBox0.Text; BOX1 = textBox1.Text; BOX2 = textBox2.Text;
            BOX3 = textBox3.Text; BOX4 = textBox4.Text; BOX5 = textBox5.Text;
            BOX6 = textBox6.Text; BOX7 = textBox7.Text; BOX8 = textBox8.Text;
            BOX9 = textBox9.Text; BOX10 = textBox10.Text; BOX11 = textBox11.Text;

            sweepA[0] = (float)Convert.ToDouble(BOX0);
            sweepA[1] = (float)Convert.ToDouble(BOX1);
            sweepA[2] = (float)Convert.ToDouble(BOX2);
            sweepA[3] = (float)Convert.ToDouble(BOX3);
            sweepA[4] = (float)Convert.ToDouble(BOX4);
            sweepA[5] = (float)Convert.ToDouble(BOX5);
            sweepA[6] = (float)Convert.ToDouble(BOX6);
            sweepA[7] = (float)Convert.ToDouble(BOX7);
            sweepA[8] = (float)Convert.ToDouble(BOX8);
            sweepA[9] = (float)Convert.ToDouble(BOX9);
            sweepA[10] = (float)Convert.ToDouble(BOX10);
            sweepA[11] = (float)Convert.ToDouble(BOX11);

            // FILL PIE ARRAY VALUES 
            //   ***************************************************************************************************************
            float sliceTotal = 0;
            for (int i = 0; i < 12; i++)//                                 
            {
                sliceTotal += sweepA[i];
            }
            // DRAWS A PIE SECTION
            Graphics myGraphics;
            Rectangle myRetcangle;
            myGraphics = panel1.CreateGraphics();
            myGraphics.SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias;
            Pen myPen;
            myPen = new Pen(Color.White, 2);
            int left = (int)(0.1 * panel1.ClientSize.Width);
            int top = (int)(0.1 * panel1.ClientSize.Height);
            int width = (int)(0.8 * panel1.ClientSize.Width);
            int height = (int)(0.8 * panel1.ClientSize.Height);
            float startA = 270;
            Brush myBrush;
            int[,] PIECOLOR = new int[12, 3] { { 253,252,59 },
                                              { 255, 0,0},
                                              { 0,255,255 },
                                              { 0,255,0 },
                                              { 128,128,128 },
                                              { 255,25,230},
                                              { 255,100,0},
                                              { 0,0,0},
                                              { 0,255,0},
                                              { 128,128,128},
                                              { 128, 128,255 },
                                              { 50,50,255 },

        };
            for (int x = 0; x < 12; x++)
            {
                float Slice = (360 / sliceTotal) * sweepA[x];
                myRetcangle = new Rectangle(left, top, width, height);
                myBrush = new SolidBrush(Color.FromArgb(PIECOLOR[x, 0], PIECOLOR[x, 1], PIECOLOR[x, 2]));// BRUSH COLOR
                myGraphics.FillPie(myBrush, myRetcangle, startA, Slice);
                myGraphics.DrawPie(myPen, myRetcangle, startA, Slice);
                startA += Slice;
            }
                    myGraphics.Dispose();
            /***********************************************************************
            * Auto scaling pie graph calculation:
            * EXAMPLE:  
            * 360 / 250 = 1.44 * 50 = 72
            * 250 = “sliceTotal”  (the complete number of items in the graph)
            * 1.44 = the conversion factor.
            * 50 = 50 items of 5 individual (even) slices.
            * 72 is the converted amount sent to the graph
            * 72 * 5 = 360
            */
            //#######################   BAR GRAPH   ################################
            // INPUTS THE TEXT BOX VALUE AND ADJUSTS FOR THE HEIGHT OF THE PANEL
            int[] BAR = new int[12];
            BAR[0] = Convert.ToInt32(BOX0);BAR[1] = Convert.ToInt32(BOX1);BAR[2] = Convert.ToInt32(BOX2);
            BAR[3] = Convert.ToInt32(BOX3);BAR[4] = Convert.ToInt32(BOX4);BAR[5] = Convert.ToInt32(BOX5);
            BAR[6] = Convert.ToInt32(BOX6);BAR[7] = Convert.ToInt32(BOX7);BAR[8] = Convert.ToInt32(BOX8);
            BAR[9] = Convert.ToInt32(BOX9);BAR[10] = Convert.ToInt32(BOX10);BAR[11] = Convert.ToInt32(BOX11);
            Rectangle myRectangle;
            myGraphics = panel2.CreateGraphics();
            // DRAW HORIZONTAL LINES  =====================
            int A1x = 0; int A2x = 400;
            int B1y = 50; int B2y = 50;
            for (int l = 0; l < 5; l++)
            {
                Graphics DrawArea2;
                DrawArea2 = panel2.CreateGraphics();
                Pen LinePen = new Pen(Color.Black  , 1);
                DrawArea2.DrawLine (LinePen, A1x, B1y, A2x, B2y);
                B1y += 50;
                B2y += 50;
            }
            //===============================================
            int xA = 20;// START OF BAR LOCATION
            int widthA = 25;// WIDTH OF BAR
            for (int j = 0; j < 12; j++)
            {
                myRectangle = new Rectangle(xA, (300 - BAR[j]), widthA, BAR[j]);
                myGraphics.FillRectangle(Brushes.LightCoral , myRectangle);// FILL
                myGraphics.DrawRectangle(Pens.Black, myRectangle);// BORDER
                xA += 30; // SPACE BETWEEN BARS
            }
            // myBrush.Dispose();
            // myGraphicsA.Dispose();
            // ######################   END BAR GRAPH       ######################
            // **********************    START LINE GRAPH   **********************
            int[] Cpoint = new int[12];
              // ________________________________________________
            Cpoint[0] = Convert.ToInt32(BOX0);
            Cpoint[1] = Convert.ToInt32(BOX1);
            Cpoint[2] = Convert.ToInt32(BOX2);
            Cpoint[3] = Convert.ToInt32(BOX3);
            Cpoint[4] = Convert.ToInt32(BOX4);
            Cpoint[5] = Convert.ToInt32(BOX5);
            Cpoint[6] = Convert.ToInt32(BOX6);
            Cpoint[7] = Convert.ToInt32(BOX7);
            Cpoint[8] = Convert.ToInt32(BOX8);
            Cpoint[9] = Convert.ToInt32(BOX9);
            Cpoint[10] = Convert.ToInt32(BOX10);
            Cpoint[11] = Convert.ToInt32(BOX11);
            //__________________________________________________________-
            int x1 = 0;//25
            int x2 = 30;//50//25
            // IT ALL WORKS
            // IT ALSO DOES RED FOR A DOWNSTAT
            for (int k = 0; k < 11; k++)
            {
                Graphics DrawArea;
                DrawArea = panel3.CreateGraphics();
                int y1 = Cpoint[k];
                int y2 = Cpoint[k + 1];
               DrawArea.SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias;//ok
              myPen.StartCap = myPen.EndCap = System.Drawing.Drawing2D.LineCap.Round;

                // DRAW HORIZONTAL LINES  =====================
                int A1=0; int A2=400;
                int B1 =25; int B2 =25 ;
                for (int l = 0; l < 15; l++)
                {
                    Pen LinePen = new Pen(Color.DarkGray  , 1);
                    DrawArea.DrawLine(LinePen, A1, B1, A2, B2);
                 B1 += 25;//50
                 B2 += 25;//50
                }
                //===============================================
                // DRAW VERTICAL LINES --------------------------
                int A11 = 30; int A22 = 30;

                int B11 = 0; int B22 = 300;

                for (int m = 0; m < 15; m++)
                {
                    Pen LinePenX = new Pen(Color.DarkGray  , 1);
                    DrawArea.DrawLine(LinePenX, A11, B11, A22, B22);

                    A11 += 30;//25 STRETCHES THE VERTICAL LINES TO 40
                    A22 += 30;//25 STRETCHES THE VERTICAL LINES TO 40
                }
                //-------------------  START LINE GRAPH  ----------------------

                // BEFORE HERE
                if (y2 < y1)
                {
                    Pen RedPen = new Pen(Color.Red, 4);
                    DrawArea.DrawLine(RedPen, x1, 300 - y1, x2, 300 - y2);
                }
                else
                {
                    Pen BlackPen = new Pen(Color.Black, 4);
                    DrawArea.DrawLine(BlackPen, x1, 300 - y1, x2, 300 - y2);
                }
                x1 += 30;
                x2 += 30;
          
                DrawArea.Dispose();
                // BlackPen.Dispose();
            }
            //  ******************    END LINE GRAPH    **********************
        // END INSIDE BUTTON
        }// END BUTTON CONTROL

        private void Form1_Load(object sender, EventArgs e)
        {
            this.Paint += new PaintEventHandler(Set_background);
        }
        private void button1_Click(object sender, EventArgs e)
        {
              this.Close();
        }
     
        private void saveFileToolStripMenuItem_Click(object sender, EventArgs e)
        {
            // SAVE FILES HERE

            string[] BOX = new string[12];
            BOX[0] = textBox0.Text;BOX[1] = textBox1.Text;BOX[2] = textBox2.Text;
            BOX[3] = textBox3.Text;BOX[4] = textBox4.Text;BOX[5] = textBox5.Text;
            BOX[6] = textBox6.Text;BOX[7] = textBox7.Text;BOX[8] = textBox8.Text;
            BOX[9] = textBox9.Text;BOX[10] = textBox10.Text;BOX[11] = textBox11.Text;
            SaveFileDialog save = new SaveFileDialog();
            save.Filter = "Text files(.txt)|*.txt|All Files|*.*";
            save.Title = "Save and Write";

            if(save .ShowDialog()==DialogResult .OK )
            {
                StreamWriter writer = new StreamWriter(save.FileName );
                for (int ax = 0; ax < 12; ax++)
                {
                     writer.WriteLine(BOX[ax] );
                }
                writer.Close();
            }
        }
        private void newOpenToolStripMenuItem_Click(object sender, EventArgs e)
        {
            // OPENS AND READ DATA INTO EACH TEXT BOX
            OpenFileDialog open = new OpenFileDialog();
            open.Filter = "Text files(.txt)|*.txt|All Files|*.*";
            open.Title = "Open and Read";
            if (open.ShowDialog() == DialogResult.OK)

            {
                StreamReader reader = new StreamReader(open.FileName);
              // LOADS THE DATA INTO THE TEXT BOXES 
                string[] BOX = new string[12];
                textBox0.Text = reader.ReadLine();textBox1.Text = reader.ReadLine();
                textBox2.Text = reader.ReadLine();textBox3.Text = reader.ReadLine();
                textBox4.Text = reader.ReadLine();textBox5.Text = reader.ReadLine();
                textBox6.Text = reader.ReadLine();textBox7.Text = reader.ReadLine();
                textBox8.Text = reader.ReadLine();textBox9.Text = reader.ReadLine();
                textBox10.Text = reader.ReadLine();textBox11.Text = reader.ReadLine();
                reader.Close();
                // CLEARS BAR GRAPH
                Graphics DrawArea;
                DrawArea = panel2.CreateGraphics();
                DrawArea.Clear(Color.White);
                //  CLEARS LINE GRAPH
                DrawArea = panel3.CreateGraphics();
                DrawArea.Clear(Color.White);
                // CLEARS PIE GRAPH
                DrawArea = panel1.CreateGraphics();
                DrawArea.Clear(Color.White);
            }
        }
     
    }AM CODE.txt…]()

# PAYROLL PROGRAM

![PAYROLL-PROGRAM](https://github.com/alvinhill/PROJECTS/assets/132315899/d3c12c3a-9ec3-407f-aac1-e5744148917b)


This is a payroll program that I am using to demonstrate inherited classes.

The parent class is “Basic”.  It is used to input the Name and Social Security Number.  I could have many fields such as: address, department, date, pay period.  What ever information that is common to all employees.  The parent class is of course used to eliminate redundant coding of the same fields in each payment category.  

The child classes inherit the Basic class.  
These classes are: Basic Commission, Salary and Hourly/Commission.  

In the basic class it is just an hourly wage transaction.   For commission, it is a percentage of the sale amount.  Salary is a flat sum with the amount dependent on the level of the employee, executive, manager of contract.  

Hourly/Commission is simply an hourly wage with the addition of a commission based on the percentage.  

The output is displayed at the bottom.  

See the video at my portfolio site: http://alvinrainhill.com/EXP-X5.html

This is just a demonstration of parent and child classes working together.  

From here I can 

Upgrade path: 

1.)	Add more info like last name, department code, date, pay period etc.
2.)	 Send the data to an SQL database and use it run queries and get reports such as department wage costs, monthly or yearly employee cost totals etc.

## Payroll Program Code

 class HOURLY
        // PARENT CLASS
    {
        public string Name { set; get; }
        public string SSN { set; get; }
        public decimal  Wage {set;get;}
        public decimal  Hours { set; get; }
        public string Getpaycat(string TYPE)
        {
            return TYPE  + "  interface data";
        }
      public virtual   decimal  GetPay(decimal  Wage, decimal  Hours)
        {
           return ( Wage *  Hours);
        }
      }
// CHILD CLASS
 class COMM :HOURLY 
        // THIS CLASS IS USING THE NAME AND SS# PROPERTIES AND OVERRIDING THE PAY METHOD
        // WITH A COMMISION METHOD 
        // THE OVERRIDING METHOD SEEMS TO NEED THE SAME NAME
        // THE OVERRIDDING METHOD MUST HAVE THE SAME NUMBER OF PARAMETERS
    {
        public decimal SalesAmt {set;get;}
        public decimal PerAmt { set; get; }
        public override  decimal GetPay(decimal SalesAmt, decimal PerAmt)

        {
            return (SalesAmt  * (PerAmt * .01m));
        }
    }




