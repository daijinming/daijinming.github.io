~~~
// Create OpenFileDialog 
Microsoft.Win32.OpenFileDialog dlg = new Microsoft.Win32.OpenFileDialog();

// Set filter for file extension and default file extension 
dlg.DefaultExt = ".png";
dlg.Filter = "JPEG Files (*.jpeg)|*.jpeg|PNG Files (*.png)|*.png|JPG Files (*.jpg)|*.jpg|GIF Files (*.gif)|*.gif";

// Display OpenFileDialog by calling ShowDialog method 
Nullable < bool > result = dlg.ShowDialog();

// Get the selected file name and display in a TextBox 
if (result == true) {
	// Open document 
	string filename = dlg.FileName;
}
~~~
