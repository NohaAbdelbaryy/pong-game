#include <SFML/Graphics.hpp>
#include <SFML/Window.hpp>
#include <sstream>
#include <iostream>
using namespace sf;	
using namespace std;
int main()
{
	//creating a window

	RenderWindow window(VideoMode(800, 600), "first game");
	window.setFramerateLimit(60);

	//shapes
	RectangleShape rectangle1(Vector2f(30, 175)), rectangle2(Vector2f(30, 175)), background(Vector2f(800, 600));
	CircleShape ball(30);
	ball.setPosition(Vector2f(350, 250));


	//text
	Font font;
	if (font.loadFromFile("pong/font.ttf"))
		cout << "font loaded\n";
	Text score;
	score.setFont(font);
	score.setCharacterSize(50);
	score.setFillColor(Color(193,0,36));
	score.setPosition(350, 20);
	

	//textures
	Texture ballT, pad, backgroundT;
	if(ballT.loadFromFile("pong/ball.png"))
		cout<<"ball loaded\n";
	if (pad.loadFromFile("pong/pad.png"))
		cout << "pad loaded\n";
	if (backgroundT.loadFromFile("pong/background.jpg"))
		cout << "bg loaded";

	//setting textures

	background.setTexture(&backgroundT);
	/*rectangle1.setTexture(&pad);
	rectangle2.setTexture(&pad);
	*/
	rectangle2.setFillColor(Color(193,0,5));
	rectangle1.setFillColor(Color(193, 0, 5));
	ball.setTexture(&ballT);


	
	//position
	rectangle2.setPosition(25, 100);
	rectangle1.setPosition(750, 100);

	//key variables
	bool up1 = false, down1 = false, down2 = false, up2 = false;
	
	int velocityY2, velocityY1,velocityXBall=6, velocityYBall=-6;
	int score1=0, score2=0;


	while (window.isOpen())
	{
		
		Event event;
		while (window.pollEvent(event))
		{
			//event processing
			if (event.type == Event::Closed)
				window.close();


			if (event.type == Event::KeyPressed)
			{
				if (event.key.code == Keyboard::Up) up1 = true;
				if (event.key.code == Keyboard::S) down2 = true;
				if (event.key.code == Keyboard::W) up2 = true;
				if (event.key.code == Keyboard::Down) down1 = true;
			}

			if (event.type == Event::KeyReleased)
			{
				if (event.key.code == Keyboard::Up) up1 = false;
				if (event.key.code == Keyboard::S) down2 = false;
				if (event.key.code == Keyboard::W) up2 = false;
				if (event.key.code == Keyboard::Down) down1 = false;
			}
		}

		//logic

		//velocity change
		if (up1 == true)
		{
			velocityY1=-5;
		}
		if (down1 == true )
		{
			velocityY1 = 5;
		}
		if (down2 == true)
		{
			velocityY2 = 5;
		}

		if (up2 == true)
		{
			velocityY2 = -5;
		}
		if ((up1 == true && down1 == true) || (up1 == false && down1 == false))
		{
			velocityY1 = 0;
		}

		if ((up2 == true && down2 == true) || (up2 == false && down2 == false))
		{
			velocityY2 = 0;
		}
		 
		if (rectangle2.getPosition().y < -30)
			rectangle2.setPosition(25, -30);

		if (rectangle2.getPosition().y > 450)
			rectangle2.setPosition(25, 450);

		if (rectangle1.getPosition().y < -30)
			rectangle1.setPosition(750, -30);

		if (rectangle1.getPosition().y > 450)
			rectangle1.setPosition(750, 450);

		if (ball.getPosition().y < 0)
			velocityYBall=-velocityYBall;

		if (ball.getPosition().y >540)
			velocityYBall = -velocityYBall;


		if (ball.getPosition().x < 0)
		{
			ball.setPosition(350, 250);
			score1++;
			velocityXBall = -velocityXBall;
		}
		if (ball.getPosition().x > 800)
		{
		
			ball.setPosition(350, 250);
			score2++;
			velocityXBall = -velocityXBall;
		}

		if (ball.getGlobalBounds().intersects(rectangle1.getGlobalBounds()) == true)
			velocityXBall = -velocityXBall;
		
		if (ball.getGlobalBounds().intersects(rectangle2.getGlobalBounds()) == true)
			velocityXBall = -velocityXBall;

		//movement
		ball.move(velocityXBall, velocityYBall);
		rectangle1.move(0, velocityY1);
		rectangle2.move(0, velocityY2);
		
		window.clear();
	
		//drawing

		window.draw(background);
		window.draw(rectangle1);
		window.draw(rectangle2);
		window.draw(ball);
		
		//string 
		stringstream padscores;
		padscores << score2 << " : " << score1;
		score.setString(padscores.str());
	
		window.draw(score); 
		window.display();
	}

	return 0;
}