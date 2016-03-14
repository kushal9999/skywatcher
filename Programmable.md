

# Introduction #
The Programmable Mount app provide a new way for user to interact with their mounts. User can now control their mounts by python script; therefore, they can DIY their own applications such as Panorama, Time Lapse, CCTV or event more with their mounts.

# User interface #
<img src='http://skywatcher.googlecode.com/files/p4.png'>

<h1>Sample Script</h1>

<h2>Sample 1 Take photos in specify positions</h2>
Taking 10 Photos in on 10 points (0,0), (20,0), (40, 0) ... (180,0)<br>
<pre><code>for i in range(10):<br>
   Controller.AddMarker(i*20, 0) # Add bookmarkers<br>
<br>
for i in Controller.GetMarkers():<br>
   Controller.Goto(i.Axis1, i.Axis2) # Goto each defined position<br>
   Controller.SetSwitch(True)        # Trigger on the camera<br>
   Controller.Sleep(1000)            # Wait 1sec<br>
   Controller.SetSwitch(False)       # Trigger off the camera<br>
</code></pre>

<h2>Sample 2 Slew the mount in low speed</h2>
<pre><code>Controller.AxisSlew(AXIS1, 1)  # Start to slew the mount's axis1 with 1 degree/sec<br>
Controller.AxisSlew(AXIS2, -1) # Start to slew the mount's axis2 with -1 degree/sec<br>
Controller.Sleep(5000)     # Let the mount slew for 5 sec<br>
Controller.AxisStop(AXIS1)     # Stop the movement on axis1<br>
Controller.AxisStop(AXIS2)     # Stop the movement on axis2<br>
</code></pre>
<h1>Controller Class</h1>
The programmable app provide a wrapper class Controller which provides high level mount control function and it can be used in the IronPython? Script environment.<br>
<br>
<br>
<h2>Mount Controller Methods</h2>
<h3><code> Init(int mount, int com) </code></h3>

Connect and Initialize the mount.<br>
<br>
Arguments:<br>
<br>
<ul><li>mount: mount's id (not support now)<br>
</li><li>com: A COM port number for serial port connection.<br>
<h3><code> AxisSlew (AXISID id, double degree) </code></h3>
Slew specify axis with a fixed speed</li></ul>

Arguments:<br>
<br>
<ul><li>axis: The target axis.<br>
</li><li>degree: The speed for movement (unit: degree).<br>
<h3><code> AxisSlewTo (AXISID id, double degree) </code></h3></li></ul>

Slew specify axis to specify position.<br>
<br>
Arguments:<br>
<br>
<ul><li>axis: The target axis.<br>
</li><li>degree: The target position for movement (unit: degree).</li></ul>

<h3><code> AxisStop (AXISID id) </code></h3>
Stop specify axis's current action<br>
<br>
Arguments:<br>
<br>
<ul><li>axis: the target axis.</li></ul>

<h3><code> SetAxisPosition (AXISID id, double degree) </code></h3>
Set current specify axis's position value.<br>
<br>
Arguments:<br>
<br>
<ul><li>axis: the target axis.<br>
</li><li>degree: the position value (unit: degree)</li></ul>

<h3><code> GetAxisPosition (AXISID id, double degree) </code></h3>
Return current axis's position value. (unit: degree) Arguments:<br>
<br>
Arguments:<br>
<br>
<ul><li>axis: the target axis.</li></ul>

<h3><code> GetAxisStatus (AXISID id) </code></h3>
Return a AXISSTATUS struct represent current axis's status<br>
<br>
Arguments:<br>
<br>
<ul><li>axis: the target axis.<br>
<h3><code> SetSwitch (bool OnOff ) </code></h3>
On/Off the trigger switch on mount. (Only apply to specify mounts)</li></ul>

Arguments<br>
<br>
<ul><li>onoff: Turn on/off the trigger switch.</li></ul>

<h2>Markers Methods</h2>
Marker method help user to use the GUI to edit / view / control the target positions of mount movements.<br>
<br>
<br>
<h3><code> InsertMarker (int index, Marker m) </code></h3>
Insert a marker in the specify index.<br>
<br>
Arguments:<br>
<br>
<ul><li>index: index of this marker.<br>
</li><li>m: the marker need to be inserted.<br>
<h3><code> AddMarker (double axis1, double axis2) </code></h3>
Append a new marker to the bookmarker list.</li></ul>

Arguments:<br>
<br>
<ul><li>axis1: the marker's axis1 position (unit: degree)<br>
</li><li>axis2: the marker's axis2 position (unit: degree)</li></ul>

<h3><code> RemoveMarkerAt (int index) </code></h3>
Remove the marker at specify index<br>
<br>
Arguments:<br>
<br>
<ul><li>index: the marker's index</li></ul>

<h3><code> RemoveMarker (Marker m) </code></h3>
Remove the marker in the list<br>
<br>
Arguments:<br>
<br>
<ul><li>m: the marker user wants to remove.<br>
<h3><code> ClearMarker () </code></h3>
Clear all markers in the list.</li></ul>


<h3><code> GetMarker (int index) </code></h3>
Return the marker at specify index<br>
<br>
Arguments:<br>
<br>
<ul><li>index: the marker's index</li></ul>

<h3><code> GetMarkers () </code></h3>
Return all markers in the marker list.<br>
<br>
<br>
<h2>Helper Method</h2>
Provide some additional support for mount control.<br>
<br>
<br>
<h3><code> Goto(double axis1, double axis2) </code></h3>
Goto the target position in synchronous mode. (method will return after the goto movements done)<br>
<br>
Arguments:<br>
<br>
<ul><li>axis1: the target position of axis1. (unit: degree)<br>
</li><li>axis2: the target position of axis2. (unit: degree)<br>
<h3><code> Sleep(int milliseconds) </code></h3>
wait for a specify time.</li></ul>

Arguments:<br>
<br>
<ul><li>milliseconds: the time (unit: milliseconds)