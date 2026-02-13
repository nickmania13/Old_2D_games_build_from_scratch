#include <SFML/Graphics.hpp>
#include <optional>
#include <cstdlib>
#include <ctime>
#include <iostream>
#include <string>
#include <sstream>
#include <vector>



using namespace std;
// Make code easier to type with "using namespace"
using namespace sf;


//Function declaration
void updateBranches(int seed);

const int NUM_BRANCHES = 6;
vector<Sprite> branches;

//Where it the player/branch?
enum class side { LEFT, RIGHT, NONE };
side branchPosition[NUM_BRANCHES];


// This is where our game starts from
int main()
{


    srand((int)time(0));


    // Get the desktop resolution
    VideoMode mode = VideoMode::getDesktopMode();

    // Create a fullscreen window (SFML 3 syntax)
    RenderWindow window;
    window.create(mode, "Timber!!!", State::Fullscreen);


    //Create a texture to hold a graphic on gpu
    Texture textureBackground;

    //Load a graphic into the te
    // xture
    if (!textureBackground.loadFromFile("graphics/graphics/background.png"))
    {
        return 1;  // Handle error
    }

    //Create a sprite and place the texture
    Sprite spriteBackground(textureBackground);

    //Set the sprite to cover the screen
    const int BACKGROUND_HORIZONTAL_POSITION = 0;
    const int BACKGROUND_VERTICAL_POSITION = 0;
    spriteBackground.setPosition({ BACKGROUND_HORIZONTAL_POSITION, BACKGROUND_VERTICAL_POSITION });

    //Make a tree sprite
    Texture textureTree;
    if (!textureTree.loadFromFile("graphics/graphics/tree.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteTree(textureTree);
    const int TREE_HORIZONTAL_POSITION = 810;
    const int TREE_VERTICAL_POSITION = 0;
    spriteTree.setPosition({ TREE_HORIZONTAL_POSITION, TREE_VERTICAL_POSITION });

    //Prepare the bee
    Texture textureBee;
    if (!textureBee.loadFromFile("graphics/graphics/bee.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteBee(textureBee);
    const int BEE_HORIZONTAL_POSITION = 0;
    const int BEE_VERTICAL_POSITION = 800;
    spriteBee.setPosition({ BEE_HORIZONTAL_POSITION, BEE_VERTICAL_POSITION });

    //Is the bee currently moving?
    bool beeActive = false;

    //How fast can the bee fly
    const float BEE_SPEED = 0.0f;
    float beeSpeed = BEE_SPEED;

    //Prepare the clouds
    Texture textureCloud;
    if (!textureCloud.loadFromFile("graphics/graphics/cloud.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteCloud1(textureCloud);
    Sprite spriteCloud2(textureCloud);
    Sprite spriteCloud3(textureCloud);

    const int CLOUD1_HORIZONTAL_POSITION = 0;
    const int CLOUD1_VERTICAL_POSITION = 0;
    const int CLOUD2_HORIZONTAL_POSITION = 0;
    const int CLOUD2_VERTICAL_POSITION = 250;
    const int CLOUD3_HORIZONTAL_POSITION = 0;
    const int CLOUD3_VERTICAL_POSITION = 500;

    spriteCloud1.setPosition({ CLOUD1_HORIZONTAL_POSITION, CLOUD1_VERTICAL_POSITION });
    spriteCloud2.setPosition({ CLOUD2_HORIZONTAL_POSITION, CLOUD2_VERTICAL_POSITION });
    spriteCloud3.setPosition({ CLOUD3_HORIZONTAL_POSITION, CLOUD3_VERTICAL_POSITION });

    //Are the clouds currently moving?
    bool cloud1Active = false;
    bool cloud2Active = false;
    bool cloud3Active = false;

    //How fast is each cloud
    const float CLOUD1_SPEED = 0.0f;
    const float CLOUD2_SPEED = 0.0f;
    const float CLOUD3_SPEED = 0.0f;

    float cloud1Speed = CLOUD1_SPEED;
    float cloud2Speed = CLOUD2_SPEED;
    float cloud3Speed = CLOUD3_SPEED;

    //Variables to control time itself
    Clock clock; // Start the clock

    //Time bar
    RectangleShape timeBar;
    float timeBarStartWidth = 400;
    float timeBarHeight = 80;
    timeBar.setSize(Vector2f(timeBarStartWidth, timeBarHeight));
    timeBar.setFillColor(Color::Red);
    timeBar.setPosition({ (1920 / 2) - timeBarStartWidth / 2 , 980 });

    Time gameTimeTotal;
    float timeRemaining = 6.0f;
    float timeBarWidthPerSecond = timeBarStartWidth / timeRemaining;



    //Track whether the game is running
    bool paused = true;





    //Load font
    Font font;
    if (!font.openFromFile("fonts/fonts/KOMIKAP.ttf"))
    {
        return 1;
    }

    //HUD text
    int score = 0;
    Text messageText(font);
    Text scoreText(font);



    

    //Assign the message and set color and size of text
    messageText.setString("Press Enter to start!");
    messageText.setCharacterSize(75);
    messageText.setFillColor(Color::White);

    scoreText.setString("Score = 0");
    scoreText.setCharacterSize(100);
    scoreText.setFillColor(Color::White);


	//Position the text
    FloatRect textRect = messageText.getLocalBounds();
    messageText.setOrigin({ textRect.position.x + textRect.size.x / 2.0f,
        textRect.position.y + textRect.size.y / 2.0f });

	messageText.setPosition({ 1920 / 2.0f , 1080 / 2.0f });
	scoreText.setPosition({ 20, 20 });



    //Prepare 6 branches and set texture for each branch sprite with a for loop
    Texture textureBranch;
    if (!textureBranch.loadFromFile("graphics/graphics/branch.png"))
    {
        return 1; //Error
    }

    for (int i = 0; i < NUM_BRANCHES; i++)  
    {
        // Create the sprite with the texture immediately
        branches.push_back(Sprite(textureBranch));

        // Now set the settings for the sprite we just added
        branches[i].setPosition({ -2000, -2000 });
        branches[i].setOrigin({ 220, 20 });

    }

    updateBranches(1);
    updateBranches(2);
    updateBranches(3);
    updateBranches(4);
    updateBranches(5);
    

    //Prepare the player
    Texture texturePlayer;
    if (!texturePlayer.loadFromFile("graphics/graphics/player.png"))
    {
        return 1;  // Handle error
    }
    Sprite spritePlayer(texturePlayer);
    const int PLAYER_HORIZONTAL_POSITION = 580;
    const int PLAYER_VERTICAL_POSITION = 720;
    spritePlayer.setPosition({ PLAYER_HORIZONTAL_POSITION, PLAYER_VERTICAL_POSITION });

    //The player starts on the left
    side playerSide = side::LEFT;


    //Prepare the gravestone
    Texture textureRIP;
    if (!textureRIP.loadFromFile("graphics/graphics/rip.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteRIP(textureRIP);
    const int RIP_HORIZONTAL_POSITION = 600;
    const int RIP_VERTICAL_POSITION = 860;
    spriteRIP.setPosition({ RIP_HORIZONTAL_POSITION, RIP_VERTICAL_POSITION });


    //Prepare the axe
    Texture textureAxe;
    if (!textureAxe.loadFromFile("graphics/graphics/axe.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteAxe(textureAxe);
    
    spriteAxe.setPosition({ 700, 830 });


    //Line up axe with the tree
    const int AXE_POSITION_LEFT = 700;
    const int AXE_POSITION_RIGHT = 1075;


    //Prepare the flying log
    Texture textureLog;
    if (!textureLog.loadFromFile("graphics/graphics/log.png"))
    {
        return 1;  // Handle error
    }
    Sprite spriteLog(textureLog);
    const int LOG_HORIZONTAL_POSITION = 810;
    const int LOG_VERTICAL_POSITION = 720;
    spriteLog.setPosition({ LOG_HORIZONTAL_POSITION, LOG_VERTICAL_POSITION });


    //Log stats
    bool logActive = false;
    float logSpeedX = 1000;
    float logSpeedY = -1500;


    //Control the player's input
	bool acceptInput = false;



    while (window.isOpen())
    {
        
        while (const std::optional<sf::Event> event = window.pollEvent())
        {
			//1.Check if X in window was clicked and close the window if it was
            if (event->is<sf::Event::Closed>())
            {
				window.close();

            }

            //2.Check if key pressed
            if (const auto& keyEvent = event->getIf<Event::KeyPressed>())
            {

                
               


                //3.Check if the key pressed was ESC
                if (keyEvent->code == Keyboard::Key::Escape)
                {
                    window.close();
                }
                
				//4.Check if the key pressed was Enter
				if (keyEvent->code == Keyboard::Key::Enter)
                {
                    paused = false;

                    //Reset time and score
                    score = 0;
                    timeRemaining = 6;


					//Make all the branches disappear
                    for (int i = 1; i < NUM_BRANCHES; i++)
                    {
                        branchPosition[i] = side::NONE;
					}

					spriteRIP.setPosition({ 675, 3000 });

                    //Move the player into position
                    spritePlayer.setPosition({ 580, 720 });
					
					acceptInput = true;



                }
            
                if (acceptInput)
                {
					if (keyEvent->code == Keyboard::Key::Right)
                    {
                        playerSide = side::RIGHT;

                        score++;

                        //Add to the time remaining
                        timeRemaining += (2 / score) + .15;
                        
                        //Move the axe to the right
                        spriteAxe.setPosition({ AXE_POSITION_RIGHT, spriteAxe.getPosition().y });
						
                        //Move the player to the right
						spritePlayer.setPosition({ 1200, 720 });
						
                        //Update the branches
						updateBranches(score);
                        
                        //Move the log flying to the left
                        logSpeedX = -5000;
                        spriteLog.setPosition({ LOG_HORIZONTAL_POSITION, LOG_VERTICAL_POSITION });
                        logActive = true;
						acceptInput = false;

					}
                    
                    if (keyEvent->code == Keyboard::Key::Left)
                    {
                        playerSide = side::LEFT;

                        score++;

                        //Add to the time remaining
                        timeRemaining += (2 / score) + .15;

                        //Move the axe to the left
                        spriteAxe.setPosition({ AXE_POSITION_LEFT, spriteAxe.getPosition().y });

                        //Move the player to the left
                        spritePlayer.setPosition({ 580, 720 });

                        //Update the branches
                        updateBranches(score);

                        //Move the log flying to the right
                        logSpeedX = 5000;
                        spriteLog.setPosition({ LOG_HORIZONTAL_POSITION, LOG_VERTICAL_POSITION });
                        logActive = true;
                        acceptInput = false;

                    }
                    
                    



                }



            }

            //5.Chech if key released
            if (const auto& keyEvent = event->getIf<Event::KeyReleased>() && !paused)
            {


                acceptInput = true;
                spriteAxe.setPosition({ 2000, spriteAxe.getPosition().y });


                }
        
        
        }
                   
        
        /***************************** Update the scene**************************/
        window.clear();

        if (!paused)
        {


            //Amount of time since last frame
            Time dt = clock.restart();


            //Subtract time
            timeRemaining -= dt.asSeconds();

            //Size up the time bar
            timeBar.setSize(Vector2f(timeBarWidthPerSecond * timeRemaining, timeBarHeight));

            //If out of time pause the game
            if (timeRemaining <= 0.0f)
            {
                paused = true;

                //Change text
                messageText.setString("Out of time !!!");


                //Reposition the text based on his new size
                FloatRect textRect = messageText.getLocalBounds();
                messageText.setOrigin({ textRect.position.x + textRect.size.x / 2.0f,
                    textRect.position.y + textRect.size.y / 2.0f });

                messageText.setPosition({ 1920 / 2.0f , 1080 / 2.0f });


            }


            //Set the bee in motion
            if (!beeActive)
            {
                //How fast is the bee
                
                beeSpeed = (rand() % 200) + 200;

                //How high is the bee
                srand((int)time(0));
                float bee_Height = (rand() % 1350) + 500;
                spriteBee.setPosition({ 2000, bee_Height });
                beeActive = true;


            }

            else
                //Move the bee when beeActive is true

            {
                // Store position in a Vector2f variable first
                Vector2f currentPositionbee = spriteBee.getPosition();

                //Calculate new position
                float newX = currentPositionbee.x - (beeSpeed * dt.asSeconds());
                float newY = currentPositionbee.y;

                //Set new position
                spriteBee.setPosition({ newX, newY });

                //Has the bee reached the leeftedge of the screen?
                if (spriteBee.getPosition().x < -100)
                {
                    //Set it up ready to be a whole new bee next frame
                    beeActive = false;
                }
            }

            //Set the clouds in action

            //Cloud1
            if (!cloud1Active)
            {
                //How fast is the cloud
                srand((int)time(0) * 10);
                cloud1Speed = (rand() % 200);

                //How high is the cloud
                srand((int)time(0) * 10);
                float cloud_Height1 = (rand() % 150);
                spriteCloud1.setPosition({ -200, cloud_Height1 });
                cloud1Active = true;

            }

            else
                //Move the cloud when cloudActive is true
            {
                // Store position in a Vector2f variable first
                Vector2f currentPositioncloud1 = spriteCloud1.getPosition();

                //Calculate the new position
                float newX = currentPositioncloud1.x + (cloud1Speed * dt.asSeconds());
                float newY = currentPositioncloud1.y;

                //Set the new position
                spriteCloud1.setPosition({ newX, newY });

                //Has the cloud reached the right side of the screen?
                if (spriteCloud1.getPosition().x > 1920)
                {
                    cloud1Active = false;
                }

            }

            //Cloud2
            if (!cloud2Active)
            {
                //How fast is the cloud
                srand((int)time(0) * 20);
                cloud2Speed = (rand() % 200);

                //How high is the cloud
                srand((int)time(0) * 20);
                float cloud_Height2 = (rand() % 300) - 150;
                spriteCloud2.setPosition({ -200, cloud_Height2 });
                cloud2Active = true;

            }

            else
                //Move the cloud when cloudActive is true
            {
                // Store position in a Vector2f variable first
                Vector2f currentPositioncloud2 = spriteCloud2.getPosition();

                //Calculate the new position
                float newX = currentPositioncloud2.x + (cloud2Speed * dt.asSeconds());
                float newY = currentPositioncloud2.y;

                //Set the new position
                spriteCloud2.setPosition({ newX, newY });

                //Has the cloud reached the right side of the screen?
                if (spriteCloud2.getPosition().x > 1920)
                {
                    cloud2Active = false;
                }

            }

            //Cloud 3
            if (!cloud3Active)
            {
                //How fast is the cloud
                srand((int)time(0) * 30);
                cloud3Speed = (rand() % 200);

                //How high is the cloud
                srand((int)time(0) * 30);
                float cloud_Height3 = (rand() % 450) - 150;
                spriteCloud3.setPosition({ -200, cloud_Height3 });
                cloud3Active = true;

            }

            else
                //Move the cloud when cloudActive is true
            {
                // Store position in a Vector2f variable first
                Vector2f currentPositioncloud3 = spriteCloud3.getPosition();

                //Calculate the new position
                float newX = currentPositioncloud3.x + (cloud3Speed * dt.asSeconds());
                float newY = currentPositioncloud3.y;

                //Set the new position
                spriteCloud3.setPosition({ newX, newY });

                //Has the cloud reached the right side of the screen?
                if (spriteCloud3.getPosition().x > 1920)
                {
                    cloud3Active = false;
                }

            }

            //Update the score text
            stringstream ss;
            ss << "Score = " << score;
            scoreText.setString(ss.str()); //sets string contained in ss to scoreText

            
            //Update the branch sprites
            for (int i = 0; i < NUM_BRANCHES; i++)
            {
                float height = i * 150;

                if (branchPosition[i] == side::LEFT)
                {
                    branches[i].setPosition({ 610, height });

                    branches[i].setRotation(degrees(180));
                
                }
                
                else if (branchPosition[i] == side::RIGHT)
                {
                    branches[i].setPosition({ 1330, height });

                    branches[i].setRotation(degrees(0));
                }

                else
                {
                    branches[i].setPosition({ 3000, height }); //hide the sprite
                }
            }
            

            if (logActive)
            {
                // Store position in a Vector2f variable first
                Vector2f currentPositionlog = spriteLog.getPosition();

                //Calculate the new position
                float newX = currentPositionlog.x + (logSpeedX * dt.asSeconds());
                float newY = currentPositionlog.y;

                //Set the new position
                spriteLog.setPosition({ newX, newY });

                //Has the log reached the right/left side of the screen?
                if (spriteLog.getPosition().x > 2000 || spriteLog.getPosition().x < -100)
                {
                    logActive = false;
                    spriteLog.setPosition({ 810,720 });
                }
                

            }


            //Has the player been squished by a branch?
            if (branchPosition[5] == playerSide)
            {

                //Pause the game
                paused = true;
                acceptInput = false;

                //Set the gravestone
                spriteRIP.setPosition({ 525, 760 });


                //Hide the player
                spritePlayer.setPosition({ 2000, 660 });

                //Change the text
                messageText.setString("SQUISHED!!");

                //Reposition the text based on his new size
                FloatRect textRect = messageText.getLocalBounds();
                messageText.setOrigin({ textRect.position.x + textRect.size.x / 2.0f,
                    textRect.position.y + textRect.size.y / 2.0f });

                messageText.setPosition({ 1920 / 2.0f , 1080 / 2.0f });
            
            
            }

                

        }


        /************ Draw the scene*******************************/
        
        // Draw our game scene here
        window.draw(spriteBackground);
		

        //Draw the clouds
		window.draw(spriteCloud1);
		window.draw(spriteCloud2);
		window.draw(spriteCloud3);

        
        //Draw the branches
        for (int i = 0; i < NUM_BRANCHES; i++)
        {
            window.draw(branches[i]);
        }


        //Draw the tree
		window.draw(spriteTree);

        //Draw player
        window.draw(spritePlayer);
        
        //Draw axe
        window.draw(spriteAxe);

        //Draw flying log
        window.draw(spriteLog);

        //Draw the gravestone
        window.draw(spriteRIP);


		//Draw the bee
		window.draw(spriteBee);

        //Draw the score
        window.draw(scoreText);
        
        //Draw the timebar
        window.draw(timeBar);
        
        
        //Draw the message
        if (paused)
        {
            window.draw(messageText);

        }
        

        


        // Show everything we just drew window.display();
        window.display();

    }

    

    return 0;
}

//Branch function definition
void updateBranches(int seed)
{
    //Move all the branches down one place
    for (int j = NUM_BRANCHES - 1; j > 0; j--)
    {
        branchPosition[j] = branchPosition[j - 1];
        
    }


    //Spawn a new branch at the top
    srand((int)time(0) + seed);
    int r = (rand() % 5);

    switch (r)
    {
    case 0:
        branchPosition[0] = side::LEFT;
        break;

    case 1:
        branchPosition[0] = side::RIGHT;
        break;

    default:
        branchPosition[0] = side::NONE;
        break;


    }


}





