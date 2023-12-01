# Allow GUI Apps

First build the Docker image

```bash
sudo docker build -t gui .  
```

then run the Docker container using the command

```bash
sudo docker run -it --net host --gpus 'all,"capabilities=compute,utility,graphics"' --privileged -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix --name gui_container gui:latest
```

You can test the GUI application 

```bash
python3 -m mujoco.viewer
```