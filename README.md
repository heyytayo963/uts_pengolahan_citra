# Uts_Pengolahan_Citra

Local URL: http://localhost:8501
  Network URL: http://192.168.1.10:8501

  
1. UPLOAD GAMBAR
```
st.title('Aplikasi Manipulasi Gambar')

# Upload gambar
uploaded_file = st.file_uploader("Pilih gambar...", type=["jpg", "jpeg", "png"])
```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/ba5143da-5f5d-4b74-a7a3-8653523aa0f4)
2. MEMBACA GAMBAR ASLI
```
if uploaded_file is not None:
    # Membaca gambar yang diunggah
    image = Image.open(uploaded_file)
    img_array = np.array(image)

    st.image(image, caption='Gambar asli', use_column_width=True)
 # Convert RGB to HSV
    hsv_image = cv2.cvtColor(img_array, cv2.COLOR_RGB2HSV)
    st.image(hsv_image, caption='Gambar dalam HSV', use_column_width=True)
```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/d67ae79d-34a4-46cd-8461-d73db9f0dcc0)
3. MENGUBAH RGB to HSV 
```
# Convert RGB to HSV
    hsv_image = cv2.cvtColor(img_array, cv2.COLOR_RGB2HSV)
    st.image(hsv_image, caption='Gambar dalam HSV', use_column_width=True)
```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/ae751437-1713-4b05-8b3b-42d8d4dc99fd)
4. MENGHITUNG HISTOGRAM
```
# Menghitung Histogram
    def plot_histogram(image):
        color = ('b', 'g', 'r')
        for i, col in enumerate(color):
            hist = cv2.calcHist([image], [i], None, [256], [0, 256])
            plt.plot(hist, color=col)
            plt.xlim([0, 256])
        plt.title('Histogram')
        plt.xlabel('Pixel Value')
        plt.ylabel('Frequency')
        st.pyplot(plt)

    st.subheader('Histogram Gambar')
    plot_histogram(img_array)

```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/4f660d7f-91cf-4720-acbb-f9ceb53a29fa)
5. MENGUBAH BRIGHTNESS DAN CONTRAST
```
# Adjust Brightness and Contrast
    st.subheader('Pengaturan Kecerahan dan Kontras')
    alpha = st.slider('Kontras', 1.0, 3.0, 1.0)
    beta = st.slider('Kecerahan', 0, 100, 0)
    adjusted = cv2.convertScaleAbs(img_array, alpha=alpha, beta=beta)
    st.image(adjusted, caption='Gambar dengan Kecerahan dan Kontras Disesuaikan', use_column_width=True)
```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/436ce4d4-36ff-4fa0-bf9c-e8ba4fa921f6)
6. MENAMPILKAN KONTUR
```
 # Menampilkan Kontur
    st.subheader('Deteksi Kontur')
    gray_image = cv2.cvtColor(img_array, cv2.COLOR_RGB2GRAY)
    blurred = cv2.GaussianBlur(gray_image, (5, 5), 0)
    edged = cv2.Canny(blurred, 50, 150)
    contours, _ = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    contour_img = img_array.copy()
    cv2.drawContours(contour_img, contours, -1, (0, 255, 0), 2)
    st.image(contour_img, caption='Gambar dengan Kontur', use_column_width=True)
```
![image](https://github.com/heyytayo963/uts_pengolahan_citra/assets/115687740/15243ea3-04c6-4560-805f-0a62fdb66150)
