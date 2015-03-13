This program can generate theorems of the MIU-system, and has a menu system which allows you to select which valid rules of inference to apply.

The program saves derivations to .txt file.

The program uses arithmetical rules of inference, with the system ported over to number theory using Godel Numbering.

I wrote this program whilst studying the book by Douglas Hofstadter, Godel, Escher & Bach...an eternal braid.

// The MIU-System Theorem Generator by Thomas Farkas, July 2013
// Ported from OPL with added derivation save feature.

import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.math.BigInteger;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class Main {

> public static int ruleinfraction;

> public static void main(String[.md](.md) args) throws IOException {

> String theorem = "MI";
> int length;

> Convtonum str = new Convtonum();
> Convtostr num = new Convtostr();

> RULEI RI = new RULEI();
> RULEII RII = new RULEII();
> RULEIII RIII = new RULEIII();
> RULEIV RIV = new RULEIV();
> FileData wrt = new FileData();

> int menu = 1;

> JFrame frame = null;
> ruleinfraction = 0;

> // Main application loop

> while (menu != -1) {

> // Check to see if valid rule was used

> if (ruleinfraction == 0) {

> System.out.println(theorem);
> wrt.writer(theorem);

> }

> ruleinfraction = 0;

> // Setting up the BigInteger C variable for use in calculating rules II,III and IV
> length = (theorem.length())-1;

> // CONVERSION OF STRING TO NUMBER
> str.conversion (theorem);

> // Menu Setup

> Object[.md](.md) options = {"Rule 1","Rule 2", "Rule 3","Rule 4", "Quit"};
> > int button = JOptionPane.showOptionDialog(frame, "Select Rule of Inference:",
> > "Java MIU-System by Thomas Farkas 2013", JOptionPane.YES\_NO\_CANCEL\_OPTION,
> > JOptionPane.QUESTION\_MESSAGE, null, options, options[2](2.md));


> // Menu Selection

> if ( button == 0) {

> RI.rule1 (theorem);
> theorem = RI.rule1string;

> }

> else if ( button == 1) {

> RII.rule2 (Convtonum.convertednumber, length);
> > num.conversion (RULEII.rule2);
> > theorem = Convtostr.convertedstring;


> }

> else if ( button == 2) {

> RIII.rule3 (Convtonum.convertednumber, length);

> if (Main.ruleinfraction != 1) {

> theorem = Convtostr.convertedstring;

> }

> }

> else if ( button == 3) {

> RIV.rule4 (Convtonum.convertednumber, length);

> if (Main.ruleinfraction != 1) {

> theorem = Convtostr.convertedstring;

> }

> }


> else if ( button == 4) {

> wrt.terminator("----------------------------");
> System.exit(0);

> }

> menu ++;

> }

> }

}


class Convtonum {

> static BigInteger convertednumber;

> void conversion (String stringconvert) {

> char compare ;
> String converted = "";
> int length = stringconvert.length();
> int counter = 0;

> while (counter != length) {

> compare = stringconvert.charAt(counter);

> if (compare == 'M') {

> converted = converted + "3";

> }

> else if (compare == 'I') {

> converted = converted + "1";

> }

> else if (compare == 'U') {

> converted = converted + "0";

> }

> counter ++;

> }

> BigInteger number = new BigInteger(converted);
> convertednumber = number;

> }

}


class Convtostr {

> static String convertedstring;

> void conversion (BigInteger bignum) {

> convertedstring = bignum.toString();

> char compare;
> String converted = "";
> int length = convertedstring.length();
> int counter = 0;

> while (counter != length) {

> compare = convertedstring.charAt(counter);

> if (compare == '3') {

> converted = converted + "M";

> }

> else if (compare == '1') {

> converted = converted + "I";

> }

> else if (compare == '0') {

> converted = converted + "U";

> }

> counter ++;

> }

> convertedstring = converted;

> }

}


class RULEI {

> String rule1string;
> String invalid = "Invalid Rule";

> void rule1 (String checkend) {

> int stringlength = checkend.length();

> char character = checkend.charAt(stringlength-1);

> if (character == 'I') {

> checkend = checkend + 'U';
> rule1string = checkend;

> }

> else if (character != 'I') {

> Main.ruleinfraction = 1;
> rule1string = checkend;

> }

> }

}


class RULEII {

> static BigInteger rule2;
> private BigInteger n;
> private BigInteger three = new BigInteger("3");
> private BigInteger ten = new BigInteger("10");

> void rule2 (BigInteger Theorem, int m) {

> n = Theorem.subtract(three.multiply((ten.pow(m))));
> rule2 = ((ten.pow(m)).multiply(three.multiply(ten.pow(m)).add(n)).add(n));

> }

}


class RULEIII {

> static BigInteger rule3 = null;
> private static BigInteger rule[.md](.md) = new BigInteger [10000](10000.md);
> private BigInteger n[.md](.md) = new BigInteger [10000](10000.md);
> private BigInteger k[.md](.md)= new BigInteger [10000](10000.md);
> private BigInteger oneeleven = new BigInteger("111");
> private BigInteger ten = new BigInteger("10");
> int i;
> int v;
> int a;
> int[.md](.md) m = new int [10000](10000.md);
> int[.md](.md) u = new int [10000](10000.md);
> int e;
> int z;

> Convtostr num = new Convtostr();
> JFrame frame = null;

> void rule3 (BigInteger T, int C) {

> i = 1;
> v = 3;
> a = 0;

> label:
> do {

> // Rule III calculations
> m[i](i.md) = C-v;
> u[i](i.md) = (m[i](i.md)+v)-a;
> k[i](i.md) = T.divide((ten.pow(u[i](i.md))));
> e = m[i](i.md)+3;

> if (e < 0 || m[i](i.md) < 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> break;

> }

> n[i](i.md) = T.subtract((k[i](i.md).multiply(ten.pow(e))).add(oneeleven.multiply(ten.pow(m[i](i.md)))));
> e = m[i](i.md)+1;
> z = m[i](i.md);

> // inequality to filter out bad strings

> // "n is any natural number less than 10 ^ m"

> if (n[i](i.md).compareTo(ten.pow(m[i](i.md))) > 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> continue label;

> }

> if (n[i](i.md).compareTo(BigInteger.ZERO) < 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> continue label;

> }

> // rule III calculation
> rule[i](i.md) = (k[i](i.md).multiply(ten.pow(e))).add(n[i](i.md));

> if (rule[i](i.md) == rule[i-1]) {

> i ++;
> v ++;
> a ++;

> rule3 = null;
> continue label;

> }

> // convert rule[i](i.md) to string for menu display
> num.conversion (rule[i](i.md));

> // Menu Setup
> Object[.md](.md) options = {"NO","YES"};
> > int button = JOptionPane.showOptionDialog(frame, Convtostr.convertedstring,
> > "SELECT THIS THEOREM?", JOptionPane.YES\_NO\_CANCEL\_OPTION,
> > JOptionPane.QUESTION\_MESSAGE, null, options, options[1](1.md));


> // Menu Selection
> if ( button == 0) {

> i ++;
> v ++;
> a ++;

> rule3 = null;
> continue label;

> }

> else if ( button == 1) {

> Main.ruleinfraction = 0;
> rule3 = rule[i](i.md);
> break;

> }

> i ++;
> v ++;
> a ++;

> } while (v != C+1);

> if (rule3 == null) {

> Main.ruleinfraction = 1;

> }

> }
}


class RULEIV {

> static BigInteger rule4 = null;
> private static BigInteger rule[.md](.md) = new BigInteger [10000](10000.md);
> private BigInteger n[.md](.md) = new BigInteger [10000](10000.md);
> private BigInteger k[.md](.md)= new BigInteger [10000](10000.md);
> private BigInteger ten = new BigInteger("10");
> int i;
> int v;
> int a;
> int[.md](.md) m = new int [10000](10000.md);
> int[.md](.md) u = new int [10000](10000.md);
> int e;
> int x;
> int y;
> int z;

> Convtostr num = new Convtostr();
> JFrame frame = null;

> void rule4 (BigInteger T, int C) {


> i = 1;
> v = 2;
> a = 0;

> label:
> do {

> // Rule IV calculations
> m[i](i.md) = C-v;
> u[i](i.md) = (m[i](i.md)+v)-a;
> k[i](i.md) = T.divide((ten.pow(u[i](i.md))));
> e = m[i](i.md)+2;

> if (e < 0 || m[i](i.md) < 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> break;

> }

> n[i](i.md) = T.subtract((k[i](i.md).multiply(ten.pow(e))));
> e = m[i](i.md);

> // inequalities to filter out bad strings

> if (n[i](i.md).compareTo(BigInteger.ZERO) < 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> continue label;

> }

> if (m[i](i.md) < 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> continue label;

> }


> // "n is any natural number less than 10 ^ m"

> if (n[i](i.md).compareTo(ten.pow(m[i](i.md))) > 0) {

> i ++;
> v ++;
> a ++;

> Main.ruleinfraction = 1;
> continue label;

> }

> // rule IV calculation
> rule[i](i.md) = (k[i](i.md).multiply(ten.pow(e))).add(n[i](i.md));

> if (rule[i](i.md) == rule[i-1]) {

> i ++;
> v ++;
> a ++;

> rule4 = null;
> continue label;

> }

> // convert rule[i](i.md) to string for menu display
> num.conversion (rule[i](i.md));

> // Menu Setup
> Object[.md](.md) options = {"NO","YES"};
> > int button = JOptionPane.showOptionDialog(frame, Convtostr.convertedstring,
> > "SELECT THIS THEOREM?", JOptionPane.YES\_NO\_CANCEL\_OPTION,
> > JOptionPane.QUESTION\_MESSAGE, null, options, options[1](1.md));


> // Menu Selection
> if ( button == 0) {

> i ++;
> v ++;
> a ++;

> rule4 = null;
> continue label;

> }

> else if ( button == 1) {

> Main.ruleinfraction = 0;
> rule4 = rule[i](i.md);
> break;

> }

> i ++;
> v ++;
> a ++;

> } while (v != C+1);

> if (rule4 == null) {

> Main.ruleinfraction = 1;

> }

> }


}


> class FileData {

> String file\_name = "C:/Users/M Mode/MIU.txt";

> void writer (String noted) throws IOException {

> //======================================
> //           WRITE TO A FILE
> //======================================
> WriteFile data = new WriteFile( file\_name );
> data.writeToFile(noted);

> }


> void terminator (String finish) throws IOException {

> WriteFile endline = new WriteFile( file\_name );
> endline.writeToFile(finish);

> }


> }


> class WriteFile {

> private String path;
> // set append\_to\_file as false for erasing/overwriting file or true for append to file
> private boolean append\_to\_file = true;

> public WriteFile(String file\_path)  {

> path = file\_path;

> }

> public WriteFile( String file\_path , boolean append\_value ) {

> path = file\_path;
> append\_to\_file = append\_value;

> }

> public void writeToFile( String textLine ) throws IOException {

> FileWriter write = new FileWriter( path , append\_to\_file);
> PrintWriter print\_line = new PrintWriter( write );
> print\_line.printf( "%s" + "%n" , textLine);
> print\_line.close();

> }

> }