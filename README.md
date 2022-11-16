# Tools

-Links-

https://www.lightinthebox.com/ro/p/barbati-hanorac-cu-gluga-grafic-florale-cranii-casual-zilnic-sfarsit-de-saptamana-tiparire-3d-casual-hanorace-hanorace-albastru-piscina-trifoi-rosu-ap_p8885813.html?prm=1.3.0.3


-C# Code-

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Net;
using System.Text;
using System.Threading.Tasks;

namespace LabelSim
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter Upper Text");
            var input1 = Console.ReadLine();
            Console.WriteLine("Enter Bottom Text");
            var input2 = Console.ReadLine();
            Console.WriteLine("Enter QR Code");
            var input3 = Console.ReadLine();
            Console.WriteLine("Connecting to printer...");

            Print(input1, input2, input3);
        }

        static bool Print(string input1, string input2, string input3)
        {
            string ipAddress = "192.168.34.249";
            int port = 6101;

            string labeltext = "^XA" + Environment.NewLine +
                " " + Environment.NewLine +
                "^FWR" + Environment.NewLine +
                " " + Environment.NewLine +
                "^CF0,100" + Environment.NewLine +
                "^FO210,70^FD" + input1 + "^FS" + Environment.NewLine +
                " " + Environment.NewLine +
                "^CF0,45" + Environment.NewLine +
                "^FO40,60^FD" + input2 + "^FS" + Environment.NewLine +
                " " + Environment.NewLine +
                " " + Environment.NewLine +
                "^FO130,376" + Environment.NewLine +
                "^BQN,0,88,H" + Environment.NewLine +
                "^FD&gt" + input3 + "^FS" + Environment.NewLine +
                " " + Environment.NewLine +
                "^XZ";


            try
            {
                // Open connection
                System.Net.Sockets.TcpClient client = new System.Net.Sockets.TcpClient();
                client.Connect(ipAddress, port);

                // Write ZPL String to connection
                StreamWriter writer = new StreamWriter(client.GetStream());
                writer.Write(labeltext);
                writer.Flush();

                // Close Connection
                writer.Close();
                client.Close();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex + "\n\n\nCONEXIUNEA LA PRINTER NU A PUTUT FI REALIZATA!");
                return false;
            }
            return true;
        }
    }
}
