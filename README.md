# godot mkdir my-godot-project
cd my-godot-project

cat > .gitignore <<'EOF'
# Godot 4+ specific ignores
.import/
.export_templates/
.godot/
*.translation

# OS-specific
.DS_Store
Thumbs.db

# Editor directories
.vscode/
.idea/

# Build artifacts
bin/
build/
dist/

# Logs
*.log
EOF

cat > Dockerfile <<'EOF'
FROM barichello/godot-ci:4.2

WORKDIR /project
COPY . /project

CMD ["bash", "-lc", "godot4 --headless --path /project --quit"]
EOF

cat > main.gd <<'EOF'
extends Control

func _ready():
    var label = Label.new()
    label.text = "Hello, Godot!"
    label.position = Vector2(100, 100)
    label.add_theme_font_size_override("font_size", 32)
    add_child(label)
EOF

cat > main.tscn <<'EOF'
[gd_scene load_steps=2 format=3]

[ext_resource type="Script" path="res://main.gd" id="1"]

[node name="Root" type="Control"]
layout_mode = 3
anchors_preset = 15
anchor_right = 1.0
anchor_bottom = 1.0
grow_horizontal = 2
grow_vertical = 2
script = ExtResource("1")
EOF

cat > project.godot <<'EOF'
; Engine configuration file.
; It's best edited using the editor if possible.

config_version=5

[application]

config/name="My Godot Project"
run/main_scene="res://main.tscn"
config/features=PackedStringArray("4.2")
EOF

git init
git add .
git commit -m "Initial Godot project"
git branch -M main

# Replace with your actual GitHub repo URL
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git

# If the repo already exists on GitHub, push:
git push -u origin main
trying new things 
