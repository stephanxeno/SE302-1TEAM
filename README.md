# Project GAME
Б.Батбаяр/B150910030/-ПХ-2 
Д.Төгсжаргал/B150910030/-ПХ-2
С.Сэнгүм/B150910060/-ПХ-2
Б.Номунбилэг/J.SE13DO12/
============Manai togloomiig yg udirdah heseg shuu==========================
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PushBlocks
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.CursorVisible = false;
            DrawDisplay d = new DrawDisplay();
            d.DrawMap();
            Player player = new Player(5,5);
            d.DrawPlayer(player);
            
            ConsoleKeyInfo keyInfo;
            while ((keyInfo = Console.ReadKey(true)).Key != ConsoleKey.Escape)
            {
                switch (keyInfo.Key)
                {
                    case ConsoleKey.RightArrow:
                        if (player.X < (Map.maparr.GetLength(1) - 1) - player.WIDTH)
                        {
                            player.Move(1, 0);
                        }
                        break;

                    case ConsoleKey.LeftArrow:
                        if (player.X > Map.maparr.GetLength(1) - (Map.maparr.GetLength(1) - 1))
                        {
                            player.Move(-1, 0);
                        }
                        break;
                    case ConsoleKey.UpArrow:
                        if (player.Y > Map.maparr.GetLength(1) - (Map.maparr.GetLength(1) - 1))
                        {
                            player.Move(0, -1);
                        }
                        break;
                    case ConsoleKey.DownArrow:
                        if (player.Y > Map.maparr.GetLength(1) - (Map.maparr.GetLength(1) - 1))
                        {
                            player.Move(0,1);
                        }
                        break;
                }
              }
         }
    }
}
====================================================================

==================Togloomiin Player iin heseg ======================
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PushBlocks
{
    public class Player
    {
        public int X { get; set; } // x coordinat
        public int Y { get; set; } // y coordinat
        public int LENGTH = 1; // mashinii urt
        public int WIDTH = 1;// mashinii orgon

        public string[,] playerbody = new string[,]
        {
            {"$"}
        };
        public Player(int x, int y)
        {
            this.X = x;
            this.Y = y;
        }
        public void Move(int x, int y)
        {
            X += x;
            Y += y;
            DrawDisplay d = new DrawDisplay();
            d.DrawPlayer(this);

            for (int i = 0; i < LENGTH; i++)
            {
                if (x == -1)
                {
                    Console.SetCursorPosition(X + WIDTH, Y + i);
                }
                else
                    Console.SetCursorPosition(X - 1, Y + i);
                Console.Write(" ");
                if (y == -1)
                {
                    Console.SetCursorPosition(Y + LENGTH, X + i);
                }
                else
                    Console.SetCursorPosition(Y - 1, X + i);
                Console.Write(" ");
            }
        }
    }
}
===========================================================================


==============Draw hiij bga heseg Player, map , 2 oo draw hiij bga odoo block iig hiih heregtei bna ======
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PushBlocks
{
    public class DrawDisplay
    {
        public void DrawMap()
        {
            int maplenght = 10;
            int mapwidth = 30;
            Map.maparr = new string[maplenght, mapwidth];

            for (int i = 0; i < Map.maparr.GetLength(0); i++)
            {
                for (int j = 0; j < Map.maparr.GetLength(1); j++)
                {
                    if (i == 0 || i == Map.maparr.GetLength(0) - 1 || j == 0 || j == Map.maparr.GetLength(1) - 1)
                    {
                        Console.ForegroundColor = ConsoleColor.White;
                        Map.maparr[i, j] = "■";
                    }
                    else
                    {
                        Map.maparr[i, j] = " ";
                    }
                    Console.Write(Map.maparr[i, j]);
                }
                Console.WriteLine();
            }
        }
        public void DrawPlayer(Player player)
        {
            for (int i = 0; i < player.LENGTH; i++)
            {
                for (int j = 0; j < player.WIDTH; j++)
                {
                    Console.SetCursorPosition(player.X, player.Y);
                    Console.ForegroundColor = ConsoleColor.White;
                    Console.Write(player.playerbody[i, j]);
                    player.X++;
                }
                player.Y++;
                player.X -= player.WIDTH;
            }
            player.Y -= player.LENGTH;
        }
        public void DrawBlocks()
        {
        }
    }
}
=============================================================

===============Map==================    Eniig shineer oruulj ogoh hereg garsaan eniig oruulj ogvol arai amarhan bsin :D
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace PushBlocks
{
    class Map
    {
        public static string[,] maparr;
    }
}
