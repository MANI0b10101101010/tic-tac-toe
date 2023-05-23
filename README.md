# tic-tac-toe
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace بازی_دوز
{
    public partial class Form1 : Form
    {
        /*
        In this program, toplay1 and toplay 2 are used to count the number of clicks,
        isplayed1 and isplayed2 are two Boolean values ​​to recognize the turns between players,
        player1sc and player2sc are used for scoring.
        ThE nameS ( player1win AND player2win AND equalgame)  is used to specify the number of wins, losses and ties .
        */
        public int player1win = 0;
        public int player2win = 0;
        public int equalgame = 0;
        public bool isPlayed1 = true;
        public bool isPlayed2 = true;
        public int toPlay1 = 0;
        public int toPlay2 = 0;
        public int player1sc = 0;
        public int player2sc = 0;
        //Here is a 3 by 3 two-dimensional presentation that will help us play our game later with some interesting tricks
        int[,] xo = new int[3, 3] { { 0, 0, 0 }, { 0, 0, 0 }, { 0, 0, 0 } };
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            
        }
        private void button2_Click(object sender, EventArgs e)
        {
           
            MessageBox.Show("  Greetings to the world, dose game is one of the simplest and at the same time one of the most entertaining games in the world that can be played. Therefore, to play the game, it is enough for the first player to start playing on the desired house with the left click, and the next player with the right click, tries to make the next move until the game ends AND This name (dwlt) is used to specify the number of wins, losses and ties"  , MessageBoxIcon.Information.ToString());
        }
        private void lbl_click(object sender, MouseEventArgs e)
        {
            /*
             In the mouse click event, we define two variables named i and j ,
             using converting the name of the third house from the label (Visual Studio sees almost everything as a array, even the names of the labels) into a string
             and then converting all In the cases mentioned, we can number our i and j variables as integers.
             Keep in mind that by doing this we adapt our array with i and j and use it in the best way. 
            */
            int i, j;
            i = int.Parse(((Label)sender).Name[3].ToString());
            j = int.Parse(((Label)sender).Name[4].ToString());
            if (e.Button == MouseButtons.Left)
            {
                if (isPlayed1 == true && xo[i, j] == 0)
                {

                    isPlayed1 = false;
                    ((Label)sender).Text = "O" ;
                    ((Label)sender).ForeColor = Color.Blue ;
                    xo[i, j] = 1;
                    check(i, j, 1, sender, e);
                    toPlay1++;
                    Console.WriteLine("1" + toPlay1);
                    isPlayed2 = true;
                    nonOfThem();
                }
            }
            else
            {
                if (isPlayed2 == true && xo[i, j] == 0)
                {

                    isPlayed2 = false;
                    ((Label)sender).Text = "X";
                    ((Label)sender).ForeColor = Color.Red;
                    xo[i, j] = 2;
                    check(i, j, 2 , sender , e);
                    toPlay2++;
                    Console.WriteLine("2" + toPlay2);
                    isPlayed1 = true;
                    nonOfThem();
                }
            }
        }
        public void check(int i, int j, int person , object sender, MouseEventArgs e)
        {
            rowcheck(i, j, person , sender , e);
            colcheck(i, j, person, sender, e);
            maindiameter(person, sender, e);
            Subdiameter(person , sender, e);
            nonOfThem();
            /*
              In the check method, we used 5 other methods to determine the winning person, which has several arguments, such as:
              person, which is the number of our player, who leaves 1 or 2 by left or right clicking on the labels in the desired house in the presentation.
              And also the two parameters i and j that we described earlier.
             */
        }
        public void rowcheck(int i, int j, int person , object sender, MouseEventArgs e)
        {
            if (xo[i, 0] == person && xo[i, 1] == person && xo[i, 2] == person)
            {
                if (i == 0)
                {
                    lbl00.BackColor = Color.Lime; lbl01.BackColor = Color.Lime; lbl02.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc += 1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++;
                    }
                }
                else if (i ==  1)
                {
                    lbl10.BackColor = Color.Lime; lbl11.BackColor = Color.Lime; lbl12.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc += 1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++;
                    }
                }
                else 
                {
                    lbl20.BackColor = Color.Lime; lbl21.BackColor = Color.Lime; lbl22.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc += 1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++; ;
                    }
                }
            }
        }
        public void colcheck(int i, int j, int person , object sender, MouseEventArgs e)
        {
            if (xo[0, j] == person && xo[1, j] == person && xo[2, j] == person)
            {
                if (j == 0)
                {
                    lbl00.BackColor = Color.Lime; lbl10.BackColor = Color.Lime; lbl20.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc += 1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++;
                    }
                }
                else if (j == 1)
                {
                    lbl01.BackColor = Color.Lime; lbl11.BackColor = Color.Lime; lbl21.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc +=1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++;
                    }
                }
                else 
                {
                    lbl02.BackColor = Color.Lime; lbl12.BackColor = Color.Lime; lbl22.BackColor = Color.Lime;
                    MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                    clearboy();
                    if (person == 1)
                    {
                        player1sc += 1;
                        lblsc1.Text = player1sc.ToString();
                        toPlay1 -= 1;
                        player1win++;
                    }
                    if (person == 2)
                    {
                        player2sc += 1;
                        lblsc2.Text = player2sc.ToString();
                        toPlay2 -= 1;
                        player2win++;
                    }
                }
            }
        }
        public void maindiameter(int person , object sender, MouseEventArgs e)
        {
            if (xo[0, 0] == person && xo[1, 1] == person && xo[2, 2] == person)
            {
                lbl00.BackColor = Color.Lime; lbl11.BackColor = Color.Lime; lbl22.BackColor = Color.Lime;
                MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                clearboy();
                if (person == 1)
                {
                    player1sc += 1;
                    lblsc1.Text = player1sc.ToString();
                    toPlay1 -= 1;
                    player1win++;
                }
                if (person == 2)
                {
                    player2sc += 1;
                    lblsc2.Text = player2sc.ToString();
                    toPlay2 -= 1;
                    player1win++;
                }
            }
        }
        public void Subdiameter(int person , object sender, MouseEventArgs e)
        {
            if (xo[2, 0] == person && xo[1, 1] == person && xo[0, 2] == person)
            {
                lbl20.BackColor = Color.Lime; lbl11.BackColor = Color.Lime; lbl02.BackColor = Color.Lime;
                MessageBox.Show("بازیکن شماره" + person.ToString() + " برنده شد");
                clearboy();
                if (person == 1)
                {
                    player1sc += 1;
                    lblsc1.Text = player1sc.ToString();
                    toPlay1 -= 1;
                    player1win++;
                }
                if (person == 2)
                {
                    player2sc += 1;
                    lblsc2.Text = player2sc.ToString();
                    toPlay2 -= 1;
                    player2win++;
                }
            }
        }
        public void nonOfThem()
        {
            if (toPlay2 + toPlay1 == 9)
            {
                MessageBox.Show("بازی مساوی شد");
                clearboy();
                player1sc += 1;
                player2sc += 1;
                lblsc1.Text = player1sc.ToString();
                lblsc2.Text = player2sc.ToString();
                equalgame++;
            }
        }
        public void clearboy()
        {
            toPlay1 = 0;
            toPlay2 = 0;
            lbl00.Text = null; lbl01.Text = null; lbl02.Text = null; lbl10.Text = null; lbl11.Text = null; lbl12.Text = null; lbl20.Text = null; lbl21.Text = null; lbl22.Text = null;
            xo[0, 0] = 0; xo[0, 1] = 0; xo[0, 2] = 0; xo[1, 0] = 0; xo[1, 1] = 0; xo[1, 2] = 0; xo[2, 0] = 0; xo[2, 1] = 0; xo[2, 2] = 0;
            isPlayed1 = true;
            isPlayed2 = true;
            lbl00.BackColor = Color.White; lbl01.BackColor = Color.White; lbl02.BackColor = Color.White; lbl10.BackColor = Color.White; lbl11.BackColor = Color.White; lbl12.BackColor = Color.White; lbl20.BackColor = Color.White; lbl21.BackColor = Color.White; lbl22.BackColor = Color.White;
        }
        private void btnClear_Click(object sender, EventArgs e)
        {
            clearboy();
        }

        private void CITGBTN_Click(object sender, EventArgs e)
        {
            MessageBox.Show(" The number of wins of the first player: " + player1win +"\n"+ " The number of wins of the secend player: " + player2win + "\n" + " The number of equal of the game : " + equalgame);
        }

        private void CLEARALL_Click(object sender, EventArgs e)
        {
            DialogResult result;
            result =  MessageBox.Show("Do you want to refresh everything even the points?","CLEAR SCOURS", MessageBoxButtons.OKCancel);
            if(result == DialogResult.OK)
            {
                clearboy();
                player1sc = 0; player2sc = 0;
                lblsc1.Text = ""; lblsc2.Text = "";
            }
        }
    }
}
