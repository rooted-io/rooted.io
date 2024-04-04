---
layout: default
---

<img src="images/rooted.png" alt="logo" width="150" height="100" class="fade-in">  

# POSTS

Posts and articles related to cybersecurity.  

## 04/04/2024

- [*Domain Fronting*](./pages/posts/04-04-24/domain-fronting.md)
- [*Hacking Kubernetes Kubelet*](./pages/posts/04-04-24/kubernetes.md)
- [*Offensive Security Privacy*](./pages/posts/04-04-24/offsec-privacy.md)

<script>
document.addEventListener("DOMContentLoaded", function() {
  // Get all images with the class 'fade-in'
  var images = document.querySelectorAll('.fade-in');

  // Loop through them
  images.forEach(function(img) {
    // Check if the image is already loaded
    if (img.complete) {
      // If already loaded, add the 'loaded' class immediately
      img.classList.add('loaded');
    } else {
      // If not loaded yet, listen for the 'load' event
      img.addEventListener('load', function() {
        // Add a delay before adding the 'loaded' class to create the effect
        setTimeout(function() {
          // Add the class 'loaded' to the image
          img.classList.add('loaded');
        }, 500); // Adjust the delay as needed
      });
    }
  });
});
</script>



