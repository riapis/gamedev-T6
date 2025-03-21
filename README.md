### Fari Hafizh R - 2206083692

# Tutorial 6
### Game over ke main menu
1. Tambah `LinkButton` dan tambah text Main Menu atau sebagainya

2. Add script seperti `LinkButton` lainnya:
```
extends LinkButton

@export var scene_to_load: String

func _on_pressed() -> void:
	get_tree().change_scene_to_file("res://scenes/" + scene_to_load + ".tscn")
``` 

### Select stage
1. Buat scene baru `SelectStage.tscn` dengan `MarginContainer`

2. Tambah `LinkButton` untuk setiap level yang ada dan return untuk kembali ke main manu, `ColorRect` jika mau

3. Tambahkan script yang sama juga untuk berpindah scene

4. Konek `LinkButton` select stage yang ada di main menu dengan scene select stage

### Pause menu
1. Buat scene baru dengan node Control dan tambahkan `PanelContainer`

2. Dalam `PanelContainer` tambahkan `Button` resume, restart, main menu, dll.

3. Beri `AnimationPlayer` untuk memunculkan dan menghilangkan pause menu saat di pencet esc key 

4. Tambahkan Script baru pada node control yang berisi
```
extends Control

func _ready():
	$AnimationPlayer.play("RESET")


func resume():
	get_tree().paused = false
	$AnimationPlayer.play_backwards("blur")

func pause():
	get_tree().paused = true
	$AnimationPlayer.play("blur")

func input():
	if Input.is_action_just_pressed("pause") and !get_tree().paused:
		pause()
	elif Input.is_action_just_pressed("pause") and get_tree().paused:
		resume()

func _on_resume_pressed():
	resume()


func _on_restart_pressed():
	resume()
	get_tree().reload_current_scene()


func _on_main_menu_pressed():
	get_tree().change_scene_to_file("res://scenes/mainmenu.tscn")

func _process(delta):
	input()
```