import matplotlib.pyplot as plt
import matplotlib.patches as patches

# A4 kağıdı boyutları (inç olarak)
fig, ax = plt.subplots(figsize=(8.27, 11.69))

# Kullanılabilir alan (kenar boşlukları bırakılarak)
usable_width = 190  # mm
usable_height = 277  # mm

# Bina boyutları (1:50 ölçekli)
building_width = 200  # mm
building_height = 240  # mm

# Kağıdın ortasına bina yerleşimi
margin_x = (usable_width - building_width) / 2
margin_y = (usable_height - building_height) / 2

# Bina dış duvarları
building_outline = patches.Rectangle((margin_x, margin_y), building_width, building_height, 
                                     linewidth=2, edgecolor='black', facecolor='none')
ax.add_patch(building_outline)

# Kapı ve pencere ölçüleri
door_width_main = 20
door_height = 42
door_width_wc_bath = 16
door_width_other = 18
window_width_kitchen = 20
window_height_default = 30
window_width_bath = 10
window_height_bath = 20
window_width_other = 30

# Giriş kapısı
ax.add_patch(patches.Rectangle((margin_x + building_width / 2 - door_width_main / 2, margin_y), 
                               door_width_main, door_height, linewidth=1, edgecolor='red', facecolor='none'))

# Banyo kapısı
ax.add_patch(patches.Rectangle((margin_x, margin_y + building_height / 2 - door_height / 2), 
                               door_width_wc_bath, door_height, linewidth=1, edgecolor='blue', facecolor='none'))

# Diğer kapılar
ax.add_patch(patches.Rectangle((margin_x + building_width - door_width_other, 
                                margin_y + building_height / 2 - door_height / 2), 
                               door_width_other, door_height, linewidth=1, edgecolor='green', facecolor='none'))

# Pencereler
# Mutfak penceresi
ax.add_patch(patches.Rectangle((margin_x + building_width / 2 - window_width_kitchen / 2, margin_y + building_height - window_height_default), 
                               window_width_kitchen, window_height_default, linewidth=1, edgecolor='yellow', facecolor='none'))

# Banyo penceresi
ax.add_patch(patches.Rectangle((margin_x, margin_y + building_height / 2 + door_height / 2), 
                               window_width_bath, window_height_bath, linewidth=1, edgecolor='cyan', facecolor='none'))

# Diğer pencereler
ax.add_patch(patches.Rectangle((margin_x + building_width - window_width_other, margin_y + building_height - window_height_default), 
                               window_width_other, window_height_default, linewidth=1, edgecolor='magenta', facecolor='none'))

# Merdivenler ve su basman
step_height = 3.6
step_width = 6
plinth_height = 18

for i in range(5):
    step_position = (margin_x + building_width / 2 - step_width / 2, margin_y + i * step_height + plinth_height)
    ax.add_patch(patches.Rectangle(step_position, step_width, step_height, linewidth=1, edgecolor='grey', facecolor='none'))

# Düzenlemeler ve yazılar
plt.gca().set_aspect('equal', adjustable='box')
plt.axis('off')
plt.show()
