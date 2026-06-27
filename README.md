Web VPython 3.2
from vpython import *

# ----------------------------
# Konstanten
# ----------------------------
G = 6.67430e-11          # Gravitationskonstante
M = 5.972e24             # Erdmasse (kg)

R_earth = 6.371e6        # Erdradius (m)
R_moon = 1.737e6         # Mondradius (m)

dt = 1000                # Zeitschritt (s)

# ----------------------------
# Szene
# ----------------------------
scene.width = 900
scene.height = 700
scene.background = color.black
scene.range = 5e8

earth = sphere(
    pos=vector(0,0,0),
    radius=R_earth,
    texture=textures.earth
)

moon = sphere(
    pos=vector(4e8,0,0),
    radius=R_moon,
    color=color.white,
    make_trail=True,
    retain=5000
)

# ----------------------------
# Anfangsgeschwindigkeit
# (kleiner als Kreisbahngeschwindigkeit)
# ----------------------------
moon.v = vector(0,900,0)

# ----------------------------
# Simulation
# ----------------------------
while True:
    rate(300)

    # Abstand Erde -> Mond
    r = moon.pos - earth.pos

    # Newtonsche Gravitation
    F = -G * M * R_moon * r / mag(r)**3

    # Beschleunigung
    a = F / R_moon

    # Euler-Integration
    moon.v += a * dt
    moon.pos += moon.v * dt
