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

XML Serialisation ->  make from an object -> xml document, 

using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Xml.Linq;
using System.Xml.Serialization;

namespace XmlDemos
{
    public class doc 
    {
        public string title { get; set; }
        public string @abstract { get; set; }
    }
    class Program
    {
        static void Main(string[] args)
        {          
           
            Console.OutputEncoding = Encoding.Unicode;
            File.ReadAllText("new.xml");  

            var serializer = new XmlSerializer(typeof(List<doc>), new XmlRootAttribute("library"));
            // make all objects of type doc inot the List , make them XMl document with root el Library

            //IEnumerable<doc> articles = (doc[])serializer  /// DESERIALISATION 
            //    .Deserialize(File.OpenRead("new.xml"));  // Xml -> make another object

            //foreach (var article in articles
            //    .Where(x => x.@abstract.Contains("програмис") 
            //    || x.@abstract.Contains("програмир")))
            //{
            //    Console.WriteLine(article.title.Replace("Уикипедия: ", string.Empty));
            //}

            var articles = new List<doc>(); // List of objects type doc

            articles.Add(new doc()
            {
                title = "1984",
                @abstract = "Nineteen Eighty-Four: A Novel, often"
            });

            articles.Add(new doc() 
            {
               title = "The Master and Margarita", 
               @abstract = "The Master and Margarita (Russian: Мастер и Маргарита) is a novel by Russian writer Mikhail Bulgakov, written in the Soviet Union between 1928 and 1940 during Stalin's regime. A censored version was published in Moscow magazine in 1966–1967, after the writer's death. The manuscript was not published as a book until 1967, in Paris"
            });

            serializer.Serialize(File.OpenWrite("goodBooks.xml"), articles);
            // serialize -> open file goodBooks and write inside all content of the articles


        }
    }
}
///
Deserialization ->  make from XML -> another object 

