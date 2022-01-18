# MuhammadUmar_BallBlast
GameTrain Assesment Task
GenID: C3_575878
Name: Muhammad Umar

Game Name: Ball Blast

•	Add cube as a player

•	Set Ground, Background and Wall

Step 1: Create a player controller 

•	Player move right or left

•	I done this task using Input manager Horizontal direction

public float horizontalInput;

public float speed = 20;

horizontalInput = Input.GetAxis("Horizontal");

transform.Translate(Vector3.right * horizontalInput * Time.deltaTime * speed);

•	Here Speed is variable that takes the values of float to multiply the position of the GameObject.

•	Transform.Translate manage the position values.

Step 2: Limit the movement of player

•	Restrict the player into the camera view with by putting the range on x axis.

•	All the changes apply on x position the y and z remain same.

private float xRange = 14;

if (transform.position.x < -xRange)

{

transform.position = new Vector3(-xRange, transform.position.y, transform.position.z);

}

if (transform.position.x > xRange)

{

transform.position = new Vector3(xRange, transform.position.y, transform.position.z);

}

Step 3: Player Fire the Bullet

•	Take capsule GameObject as a bullet and adjust material.

•	Create bullet Prefab.

•	Instantiate the bullet by prefab.

•	Control the instantiation by Space Button

public GameObject BulletPrefab;

if (Input.GetKeyDown(KeyCode.Space))

{

Instantiate(BulletPrefab, transform.position, BulletPrefab.transform.rotation);

}

•	The bullet changes its position in y direction. For this purpose, create MoveForward.cs Script and apply action.

public float speed = 20.0f;

transform.Translate(Vector3.up * Time.deltaTime * speed);

Step 4: Destroy Bullet when leave Scene View

•	Create another script DestroyOutOfBound.cs to destroy the bullet when leave the screen.

•	This is extendable If new GameObjects added.

private float TopBound = 15.0f;

if (transform.position.y > TopBound)

{

Destroy(gameObject);

}

Step 5: Ball on the Game

•	Create Sphere GameObject as ball.

•	Apply Material on the sphere.

•	Add Text for health indicating.

•	Apply physics on Ball. 

•	Move downward and Jump on y direction by using AddForce method and all unnecessary positions and rotations set to be freeze.

private Rigidbody rbBall;

private float JumpForce = 20;

rbBall.AddForce(Vector3.up * JumpForce, ForceMode.Impulse);

•	Add tag on ground.

if (collision.gameObject.tag == "ground")

{

rbBall.AddForce(Vector3.up * JumpForce, ForceMode.Impulse);

}

Step 6: Review all physics components

•	Box Collider

•	Mesh Collider

•	Rigid Body

•	Sphere Collider

Step 7: Set health Mechanics

•	The text is already adjusted then write the code to implement.

private float health = 5;

public TMP_Text ballhealth;

void healthUpdates()

{

ballhealth.text = health.ToString();

}

Step 8: Damage and destroy ball

private void OnCollisionEnter(Collision collision)

{

if (collision.gameObject.tag == "Bullet")

{

Damage(1);

        }

if (collision.gameObject.tag == "ground")

{

rbBall.AddForce(Vector3.up * JumpForce, ForceMode.Impulse);

}

if(collision.gameObject.tag == "Player")

{

Debug.Log("Game Over");

}

}

void Damage(int bl)

{

if(health > 1)

{

health -= bl;

}else

{

ballDistroy();

}

}

void ballDistroy()

{

Destroy(gameObject);

}

Step 9: Setting SpawnManager

•	Take prefab of ball

•	Create empty Game Object named SpawnManager.

•	attach script name SpawnManager.cs 

public GameObject ballPrefab;

private float spawnRangeX = 13;

private float spawnRangeY = 10;

private float startDelay = 1;

private float TimeInterval = 4f;

InvokeRepeating("SpawnBall", startDelay, TimeInterval);

void SpawnBall()

{

Vector3 spawnPos = new Vector3(Random.Range(-spawnRangeX, spawnRangeX), spawnRangeY, 0);

Instantiate(ballPrefab, spawnPos, ballPrefab.transform.rotation);

}

Step 10: Generate the Build WebGL

Link: https://play.unity.com/mg/other/webgl-builds-137240

