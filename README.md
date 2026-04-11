# **Django Image Optimizer**

A **Django middleware and utility** for optimizing uploaded images by converting them to WebP with configurable **width, height, and quality** settings.

> *Fixed version, works with django-cabinet.*

## **Features**

✔ **Automatic optimization via middleware**  
✔ **Manual optimization via utility function**  
✔ **Supports per-request overrides**  
✔ **Configurable defaults via `settings.py`**

---

## **Installation**

```sh
pip install django-optimize-image
```

Add the middleware:

```python
MIDDLEWARE = [
    # other middleware...
    "optimizer_middleware.middleware.ImageOptimizationMiddleware",
]
```

---

## **Configuration**

Set global defaults in **`settings.py`**:

```python
# Default image optimization settings
IMAGE_OPTIMIZER_WIDTH = 800   # Resize width
IMAGE_OPTIMIZER_HEIGHT = None  # Keep aspect ratio
IMAGE_OPTIMIZER_QUALITY = 80  # WebP quality
```

> _By default, images are resized to 800px width while maintaining aspect ratio and optimized to 80% quality._

---

## **Usage**

### **1️⃣ Automatic Optimization (Middleware)**

Once added to `MIDDLEWARE`, the optimizer **automatically processes all uploaded images** in `POST`, `PUT`, and `PATCH` requests.

✅ Converts images to **WebP**  
✅ Resizes based on `settings.py`

---

### **2️⃣ Dynamic Overrides (Per Request)**

Override optimization settings dynamically in a view using **`request.META`**:

```python
def upload_view(request):
    request.META["IMAGE_OPTIMIZER_WIDTH"] = 600
    request.META["IMAGE_OPTIMIZER_QUALITY"] = 90
    return some_response
```

---

### **3️⃣ Manual Optimization (Standalone Function)**

Use the function **anywhere** in your code (views, forms, serializers, etc.).

```python
from optimizer_middleware.utils import optimize_image

optimized_image = optimize_image(image_file, width=500, quality=85)
```

---

## **License**

[MIT License](LICENSE). Free to use and modify. 🚀

---

## **Contribution**

Use this guide [Contribution](https://opensource.guide/how-to-contribute/)
