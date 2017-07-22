# Picasso Library

## Gradle

```gradle
dependencies {
    ...
    compile 'com.squareup.picasso:picasso:2.5.2'
	...
}
```

## Usage

```java
public class ShopViewHolder extends RecyclerView.ViewHolder {
	...
    public void initLayout(Context context, Shop shop) {
        this.shop = shop;
        Picasso.with(context)
                .load(shop.getImageUrl())
                .placeholder(R.drawable.place_holder)
                .into(imageView);
		...
    }
}
```