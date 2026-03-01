func _init(_path := []):
path = _path
idx = 0
pos = path[0]
health = ENEMY_HP
alive = true
func update(dt):
if not alive: return
var next_p = path[idx + 1] if idx + 1 < path.size() else null
if next_p == null:
alive = false
_on_reach_base()
return
var dir := (next_p - pos)
var dist := dir.length()
var move := speed * dt
if dist <= move:
pos = next_p
idx += 1
else:
dir = dir.normalized()
pos += dir * move
func draw():
# просто примитив
draw_circle(pos, 7, Color(0, 0.5, 0))
var hp_pct := clamp(health / ENEMY_HP, 0, 1)
draw_rect(Rect2(pos.x - 7, pos.y - 12, 14 * hp_pct, 3), Color(0, 1, 0))


