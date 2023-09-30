# onepose

Human **pose** estimation within **one line**

```bash
pip install git+https://github.com/developer0hye/onepose.git
```

```python
import cv2
import onepose
img = cv2.imread("sample.png")
keypoints = onepose.create_model().to("cuda")(img)
```

![output](https://github.com/developer0hye/onepose/assets/35001605/373de9d0-a2ea-4b34-8b6c-156e5de71377)

One Piece's Luffy pose predicted by onepose

# Examples

## Plot keypoints on an image
```python
import cv2
import onepose

if __name__ == '__main__':
    img = cv2.imread('sample.png')
    model = onepose.create_model()

    keypoints = model(img)
    num_keypoints = len(keypoints['points'])
    
    for i in range(num_keypoints):
        print(f"Point {i} (x, y)  : {keypoints['points'][i]} confidence: {keypoints['confidence'][i]}")
        
        if keypoints['confidence'][i] < 0.5:
            color = (0, 0, 255)
        else:
            color = (0, 255, 0)
        
        cv2.circle(img, (int(keypoints['points'][i][0]), int(keypoints['points'][i][1])), 5, color, -1)
    cv2.imshow('img', img)
    cv2.waitKey(0)
```

Notice that occluded key points are plotted in red. You can discard these points using confidence score.

![output](https://github.com/developer0hye/onepose/assets/35001605/efad3e3f-7ab7-4521-bec1-d5cb2f9007a2)


## Print supported models
```python
import onepose
print(onepose.list_models()) # ['ViTPose_base_simple_coco', 'ViTPose_large_simple_coco', 'ViTPose_huge_simple_coco', ...]
```

# References

[ViTAE-Transformer/ViTPose](https://github.com/ViTAE-Transformer/ViTPose)

[jaehyunnn/ViTPose_pytorch](https://github.com/jaehyunnn/ViTPose_pytorch)

[JunkyByte/easy_ViTPose](https://github.com/JunkyByte/easy_ViTPose)
