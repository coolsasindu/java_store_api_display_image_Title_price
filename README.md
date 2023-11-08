# java_store_api_display_image_Title_price
Fake Store API Fake store rest API for your e-commerce or shopping website prototype

How to use it
fakeStoreApi can be used with any type of shopping project that needs products, carts, and users in JSON format. you can use examples below to check how fakeStoreApi works and feel free to enjoy it in your awesome projects!

URL = https://fakestoreapi.com/products/1

OUTPUT = {"id":1,"title":"Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops","price":109.95,"description":"Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday","category":"men's clothing","image":"https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg","rating":{"rate":3.9,"count":120}}

java '''
public void imgload() {
    SwingWorker<ImageIcon, Void> worker = new SwingWorker<>() {
        String title, description, category;

        @Override
        protected ImageIcon doInBackground() {
            try {
                OkHttpClient client = new OkHttpClient();
                String getid = textid.getText(); // Assuming textid is a JTextField
                String apiUrl = "https://fakestoreapi.com/products/" + getid;
                Request request = new Request.Builder().url(apiUrl).build();

                Response response = client.newCall(request).execute();

                if (response.isSuccessful()) {
                    String responseData = response.body().string();
                    JSONObject jsonObject = new JSONObject(responseData);

                    title = jsonObject.getString("title");
                    description = jsonObject.getString("description");
                    category = jsonObject.getString("category");

                    String image = jsonObject.getString("image");
                    URL url = new URL(image);
                    Image addimage = ImageIO.read(url);
                    Image scaledImage = addimage.getScaledInstance(200, 200, Image.SCALE_SMOOTH);
                    return new ImageIcon(scaledImage);
                }
            } catch (IOException e) {
                e.printStackTrace(); // Proper error handling is recommended
            }
            return null;
        }

        @Override
        protected void done() {
            try {
                ImageIcon imageIcon = get();
                if (imageIcon != null) {
                    j5.setIcon(imageIcon); // Assuming j5 is a JLabel
                    j1.setText(title);
                    j2.setText(description);
                    j3.setText(category);
                    j4.setText(title);
                } else {
                    // Handle if image loading failed
                }
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    };

    worker.execute();
}
'''
'''
