# BT-arcgis
Viec 1 :
from scipy.spatial.distance import pdist
import numpy as np

# Tạo mảng chứa các điểm
X = np.array([[0, 1], [2, 2]])

# Tính toán khoảng cách Euclidean giữa các cặp điểm
distances = pdist(X, 'euclidean')

print("Khoảng cách Euclidean giữa các cặp điểm là:", distances)

Viec 2 , 3 :
#
a) Hãy xây dựng mô hình tính “nghịch đảo khoảng cách” cho trường hợp có 3 điểm trong không gian với giá trị (x,y) và giá trị đo là z và cần tính giá trị z tại điểm thứ 4 đã biết x, y. Biết rằng “khoảng cách” giữa các điểm là khoảng cách hình học.

def inverse_distance_weighting(x, y, points):
    weighted_sum = 0
    sum_of_weights = 0
    
    # Tính toán trọng số và tổng trọng số
    for px, py, pz in points:
        distance_squared = (x - px) ** 2 + (y - py) ** 2
        if distance_squared != 0:
            weight = 1 / distance_squared
            weighted_sum += weight * pz
            sum_of_weights += weight
    
    # Tránh chia cho 0
    if sum_of_weights != 0:
        return weighted_sum / sum_of_weights
    else:
        return None

# Các điểm dữ liệu (x, y, z)
points = [(1, 1.5, 1.5), (5, 7.5, 7.5)]

# Điểm cần tính giá trị z (x, y)
point_x = 2
point_y = 2

# Tính giá trị z tại điểm cần tính
result_z = inverse_distance_weighting(point_x, point_y, points)
print("Giá trị z tại điểm ({}, {}) là: {}".format(point_x, point_y, result_z))

b) Ứng dụng mô hình vừa xây dựng ở câu a hãy tính giá trị ô nhiễm dự đoán tại vị trí D(200, 100) biết rằng giá trị ô nhiễm tại 3 vị trí lần lượt là: A(100, 200) là 128, B(100, 50) là 100 và C(300, 20) là 32.
# Các điểm dữ liệu (x, y, z)
points = [(100, 200, 128), (100, 50, 100), (300, 20, 32)]

# Điểm D cần tính giá trị z (x, y)
point_x_D = 200
point_y_D = 100

# Tính giá trị z tại điểm D
result_z_D = inverse_distance_weighting(point_x_D, point_y_D, points)
print("Giá trị ô nhiễm dự đoán tại điểm D({}, {}) là: {}".format(point_x_D, point_y_D, result_z_D))

c) Viết một hàm bằng Python nhập vào 11 giá trị như trên (3 giá trị của điểm A, 3 giá trị điểm B, 3 giá trị điểm C và 2 giá trị điểm D) để tính giá trị còn lại của điểm D theo phương pháp trên. Gợi ý tên hàm là: def tinhNghichDaoKhoangCach(ax, ay, az, bx, by, bz, cx, cy, cz, dx, dy): #để tính ra dz.

def tinhNghichDaoKhoangCach(ax, ay, az, bx, by, bz, cx, cy, cz, dx, dy):
    points = [(ax, ay, az), (bx, by, bz), (cx, cy, cz)]
    result_z_D = inverse_distance_weighting(dx, dy, points)
    return result_z_D

# Nhập vào các giá trị của A, B, C và D
result_z_D = tinhNghichDaoKhoangCach(100, 200, 128, 100, 50, 100, 300, 20, 32, 200, 100)
print("Giá trị z tại điểm D là:", result_z_D)

