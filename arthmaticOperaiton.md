![image](https://github.com/user-attachments/assets/2985e96f-0cda-4a92-ace7-ba04be1a4768)

![image](https://github.com/user-attachments/assets/3aa2a689-41e4-4cd6-aa2e-4bc6133b0d2f)

Wrap- around happens when the result is too big to be stored on the shown, so it will be truncated. so only first 4 bytes are shown

Doing partial register

![image](https://github.com/user-attachments/assets/4bdf912d-fd78-4e24-94fd-81d10ced50ca)

you gotta be careful when adding partial registers compared to full registers, full registers simply overides the value to the current value being added but partial registers only modify part of it
for instance now lets say we are adding al, ch (al=FF + CH=07) which equal to **106, its a big value to store so we going to do a wrap around so its gonna be 06**
