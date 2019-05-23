# Bowling-Game
this is a normal Bowling game but i haven't finished it yet  
// Ball //
public class Ball : MonoBehaviour {
public Vector3 launchVeclocity;

private Rigidbody rigidBody;
private AudioSource audioSource;

	// Use this for initialization
	void Start () {
	rigidBody = GetComponent<Rigidbody>();
	rigidBody.useGravity = false;
	audioSource = GetComponent<AudioSource>();
	
	
	 
	}
	public void Launch()
	{
		rigidBody.velocity = launchVeclocity;
		audioSource.Play();
	}
	
	public void Launch(Vector3 velocity)
	{
		rigidBody.useGravity = true;
	rigidBody.velocity = velocity;
	
	audioSource = GetComponent<AudioSource>();
	audioSource.Play ();
	}
	
}

// CameraControle //
public class CameraControl : MonoBehaviour {

public Ball ball;

private Vector3 offset;

	// Use this for initialization
	void Start () {
	offset = transform.position - ball.transform.position;
	
	}
	
	// Update is called once per frame
	void Update () {
	if (transform.position.z <= 1829f){// In front of head pin
	
	transform.position = ball.transform.position + offset;
	}
	
	}
}

// DragLaunch //
[RequireComponent (typeof(Ball))]
public class DragLaunch : MonoBehaviour {

private Vector3 dragStart , dragEnd;
private float startTime, endTime;
private Ball ball;

	// Use this for initialization
	void Start () {
	ball = GetComponent <Ball>();
	
	}
	
	public void DragStart(){
	// capture time & position of drag start 
	dragStart = Input.mousePosition;
	startTime = Time.time;
	}
	public void DragEnd () {
	// Launch the ball
	dragEnd = Input.mousePosition;
	endTime = Time.time;
	
	float dragDuration = endTime - startTime;
	
	float launchSpeedX = (dragEnd.x - dragStart.x) / dragDuration;
	float launchSpeedZ = (dragEnd.y - dragStart.y)/ dragDuration;
	
	Vector3 launchvelocity = new Vector3 (launchSpeedX , 0 , launchSpeedZ);
	ball.Launch(launchvelocity);
	
	}
}
