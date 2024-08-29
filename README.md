Simplistic project for a Lab

package leonlinmovies;
/**Course: CSC 191
 * Project: Lab 12
 * Date: April 26, 2023
 * Author: Leon
 * Purpose: For this lab, create a GUI application that will keep a movie inventory for the user.
 */
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.border.*;
import java.text.DecimalFormat;
import java.util.LinkedList;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Scanner;
class MovieGUI extends JFrame{
    LinkedList<Movie> movie = new LinkedList<>();
    JLabel nameL;
    JTextField nameF;
    JLabel mediaL;
    JTextField mediaF;
    JLabel yearL;
    JTextField yearF;
    JButton show;
    JButton add;
    JPanel inputs;
    JTextArea outputs;
    JPanel movies;
   
    public MovieGUI(){
        createUserInterface();
    }
    private void createUserInterface(){
        Container contentPane = getContentPane();
        contentPane.setLayout(null);
       
        inputs = new JPanel();
        inputs.setLayout(null);
        inputs.setBorder(new TitledBorder("Input Movie"));
        inputs.setBounds(10,10,200,175);
        contentPane.add(inputs);
       
        nameL = new JLabel();
        nameL.setBounds(10,30,80,20);
        nameL.setText("Movie Name: ");
        inputs.add(nameL);
       
        nameF = new JTextField();
        nameF.setBounds(100,30,90,20);
        nameF.setHorizontalAlignment(JTextField.LEFT);
        inputs.add(nameF);
       
        mediaL = new JLabel();
        mediaL.setBounds(10,60,80,20);
        mediaL.setText("Media: ");
        inputs.add(mediaL);
       
        mediaF = new JTextField();
        mediaF.setBounds(100,60,90,20);
        mediaF.setHorizontalAlignment(JTextField.LEFT);
        inputs.add(mediaF);
       
        yearL = new JLabel();
        yearL.setBounds(10,90,80,20);
        yearL.setText("Year: ");
        inputs.add(yearL);
       
        yearF = new JTextField();
        yearF.setBounds(100,90,90,20);
        yearF.setHorizontalAlignment(JTextField.LEFT);
        inputs.add(yearF);
       
        add = new JButton();
        add.setBounds(75,130,115,30);
        add.setText("Add Movie");
        inputs.add(add);
       
        add.addActionListener(
            new ActionListener(){@Override
                public void actionPerformed(ActionEvent event){
                    addAction(event);
                }
            }
        );
       
        movies = new JPanel();
        movies.setLayout(null);
        movies.setBorder(new TitledBorder("Movies: "));
        movies.setBounds(230,10,310,240);
        contentPane.add(movies);
       
        outputs = new JTextArea();
        outputs.setBounds(20,20,275,210);
        outputs.setText("");
        outputs.setEditable(false);
        movies.add(outputs);
       
        show = new JButton();
        show.setBounds(420, 255, 120, 30);
        show.setText("Show Movies!");
        contentPane.add(show);
        show.addActionListener(
            new ActionListener(){ @Override
                public void actionPerformed(ActionEvent event){
                   showAction(event);
                }
            }
        );
       
        setTitle("Movie Database");
        setSize(600, 350);
        setVisible(true);
    }
    public void addAction(ActionEvent e){
        Movie m = new Movie(nameF.getText(), mediaF.getText(),Integer.parseInt(yearF.getText()));
        movie.add(m);
    }
    public void showAction(ActionEvent e){
        outputs.setText("");
        outputs.append("Year\tMedia\tTitle\n");
        for(Movie s: movie){
            outputs.append(s.year+"\t"+s.media+"\t"+s.name+"\n");
        }
    }
}
class Movie{
    String name;
    String media;
    int year;
 
    public Movie(String n, String m, int y){
        name = n;
        media = m;
        year = y;
    }
 }
// main used in order to close program with the exit button
public class LeonLinMovies {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        MovieGUI application = new MovieGUI();
        application.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }

   
}
