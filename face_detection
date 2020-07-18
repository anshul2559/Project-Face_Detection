# Write a Python Script that captures images from your webcam video stream
# Extracts all Faces from the image frame (using haarcascades)
# Stores the Face information into numpy arrays

# 1. Read and show video stream, capture images
# 2. Detect Faces and show bounding box (haarcascade)
# 3. Flatten the largest face image(gray scale) and save in a numpy array
# 4. Repeat the above for multiple people to generate training data




import cv2
import numpy as np
cap=cv2.VideoCapture(0)

face_cascade=cv2.CascadeClassifier(r"C:\Users\Admin\Desktop\coding blocks files\haarcascade_frontalface_alt.xml")
face_data=[]
dataset_path=r"../opencv/"
skip=0
filename=input("enter the name of the individual: ")
while True:
    ret,frame=cap.read()
    if ret==False:
        continue
     # when we have multiple faces
    faces=face_cascade.detectMultiScale(frame,1.3,3)
    print(faces)
    if len(faces) == 0:
        continue
    faces=sorted(faces,key=lambda f:f[2]*f[3])

    for face in faces[-1:]:
        x,y,w,h=face
        cv2.rectangle(frame,(x,y),(x+w,y+h),(255,0,0),2)

        offset=10
        face_section=frame[y-offset:y+h+offset,x-offset:x+w+offset]
        face_section=cv2.resize(face_section,(100,100))

        skip+=1
        if skip%10==0:
            face_data.append(face_section)
    cv2.imshow("Frame",frame)
    cv2.imshow("Face_section",face_section)

    key_pressed=cv2.waitKey(1) & 0xFF
    if key_pressed==ord('q'):
        break

face_data=np.asarray(face_data)
face_data=face_data.reshape(face_data.shape[0],-1)

np.save(dataset_path+filename+'.npy',face_data)
print("data successfully save at"+dataset_path+filename+'.npy')

cap.release()
cv2.destroyAllWindows()
