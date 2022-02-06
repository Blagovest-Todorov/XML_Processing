# XML_Processing
XML_Processing, 
//////////
XML -> DataFormat for storing and transportation od data, similar to Json, but is tag Language, and is more detailed and bigger volume than Json, 
XML Parse is bit slower than Json Parser.

////

using System;
using System.IO;
using System.Linq;
using System.Xml.Linq;

namespace XmlDemos
{
    class Program
    {
        static void Main(string[] args)
        {

            XDocument doc = new XDocument(); /// Create the Object XML Document

            var root = new XElement("library"); /// Create root XML Tag <library>

            doc.Add(root);   // add the root element to the XML doc

            for (int i = 0; i < 100; i++)  /// fill the Library root tag with another child elements
            {
                var book = new XElement("book");
                    root.Add(book);
                book.Add(new XElement("title", i.ToString()));
                book.Add(new XElement("price", i / 100.0));
            }

            doc.Save("new.xml");

            var str = File.ReadAllText("new.xml");

            for (int i = 0; i < str.Length; i++)
            {
                Console.Write(str[i]);
            }

            
        }
    }
}
/////////
