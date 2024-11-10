# How to Guide - Moving characters in Godot.
## This is the code needed for the How to Guide, copy and paste the code into the editor when following along the tutorial.
If you are experiencing errors when pasting code into Godot, it may be because **indentation** isn't correct, make sure to refer to the PowerPoint if you are unsure.

3.2:
```gdscript
extends Area2D

@export var speed = 400 # How fast the player will move (pixels/sec).
var screen_size # Size of the game window.
```
3.3:
```gdscript
func _ready():
	screen_size = get_viewport_rect().size
```
3.5:
```gdscript
func _process(delta):
	var velocity = Vector2.ZERO # The player's movement vector.
	if Input.is_action_pressed("move_right"):
		velocity.x += 1
	if Input.is_action_pressed("move_left"):
		velocity.x -= 1
	if Input.is_action_pressed("move_down"):
		velocity.y += 1
	if Input.is_action_pressed("move_up"):
		velocity.y -= 1

	if velocity.length() > 0:
		velocity = velocity.normalized() * speed
		$AnimatedSprite2D.play()
	else:
		$AnimatedSprite2D.stop()
```
3.6:
```gdscript
	position += velocity * delta
	position = position.clamp(Vector2.ZERO, screen_size)
```
3.7:
```gdscript
	$AnimatedSprite2D.flip_v = velocity.y > 0
	if velocity.x != 0:
		$AnimatedSprite2D.animation = "walk"
		$AnimatedSprite2D.flip_h = velocity.x < 0
	elif velocity.y != 0:
		$AnimatedSprite2D.animation = "up"
```
