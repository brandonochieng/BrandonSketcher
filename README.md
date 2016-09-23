# BrandonSketcher
package trevial;
import java.awt.Graphics;
import java.awt.Point;
import java.awt.BorderLayout;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseMotionAdapter;
import java.awt.event.MouseEvent;
import javax.swing.JFrame;
import javax.swing.JPanel;
import java.util.ArrayList;

public class trevial extends JPanel{
	private ArrayList<Point> lastPoint = new ArrayList<Point>();
	
	public trevial(){
		addMouseListener(new MouseAdapter(){
			public void mousePressed( MouseEvent e){
				lastPoint.add(new Point(e.getX(),e.getY()));
			}
		} );
		
		addMouseMotionListener(new MouseMotionAdapter(){
			public void mouseDragged(MouseEvent e){
				Graphics g = getGraphics();
				int last = lastPoint.size();
				lastPoint.add(new Point(e.getX(),e.getY()));
				g.drawLine(lastPoint.get(last-1).x, lastPoint.get(last-1).y, e.getX(), e.getY());
				g.dispose();
			}
		});
	}

	public void paint(Graphics g){
		int i=0;
		for(int j=1;j<lastPoint.size();j++){
			
			g.drawLine(lastPoint.get(i).x,lastPoint.get(i).y,lastPoint.get(j).x,lastPoint.get(j).y);
			g.dispose();
			i++;
		}
	}
	public static void main(String []args){
		JFrame frame = new JFrame("SKETCH THE DRAWING HERE");
		frame.getContentPane().add(new trevial(), BorderLayout.CENTER);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setSize(400, 300);
		frame.setVisible(true);
	}
}
