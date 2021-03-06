# Paint Application
[Programming for Beginners in C# Windows Forms](https://www.udemy.com/programming-windows-applications-for-desktop-in-c-sharp/)

&nbsp;
## 00 Start the project
* In VS, create a Windows Forms Application project.

&nbsp;
## 01 Form Initial Setup
* Set background and initial size: In the *Properties* tab, set *BackColor* to white and *Size* to 800, 600.
* From the *Toolbox*, add a *StatusStrip*.

&nbsp;
## 02 Initialize variables
* Add the *listOfPoints* and *pencilDown* variables and initialize them.
```
        ArrayList listOfPoints;
        bool pencilDown;

        public Form1()
        {
            InitializeComponent();
            listOfPoints = new ArrayList();
            pencilDown = false;
        }
```


&nbsp;
## 03 Add the *MouseDown* event
* From the *Events* tab add the *MouseDown* event. Add a *Point*, add it to the *listOfPoints* and set the *pencilDown* and *statusStrip* values accordingly.
```
    private void Form1_MouseDown(object sender, MouseEventArgs e)
        {
            Point aPoint = new Point(e.X, e.Y);
            listOfPoints.Add(aPoint);
            pencilDown = true;
            this.statusStrip1.Items[0].Text = "MouseDown";
        }
```

&nbsp;
## 04 Add the *MouseUp* event
* From the *Events* tab add the *MouseUp* event. Set the *pencilDown* and *statusStrip* values accordingly.
```
    private void Form1_MouseUp(object sender, MouseEventArgs e)
        {
            pencilDown = false;
            this.statusStrip1.Items[0].Text = "MouseUp";
        }
```

&nbsp;
## 05 Add the *MouseMove* event
* From the *Events* tab add the *MouseMove* event. Add an instance of the *Graphics* class.
Add a new *Point* and a *Pen*. When the *MouseDown* and *MouseMove* events occur concurrently, that is when *pencilDown* is true while the mouse is moving, the *statusStrip* text is set to *MouseMove* and a line is drawn between consequent points.
```
    private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            Graphics g = this.CreateGraphics();
            Point newPoint = new Point(e.X, e.Y);
            Pen pencil = new Pen(Color.Blue);

            if (pencilDown)
            {
                this.statusStrip1.Items[0].Text = "MouseMove";
                g.DrawLine(pencil, (Point)listOfPoints[listOfPoints.Count - 1], newPoint);
                listOfPoints.Add(newPoint);
            }

        }
```
