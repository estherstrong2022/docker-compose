version: '2'

services:
  ui:
    build: ./ui-web-app-reactjs
    ports:
      - 8080:8080

  zuul:
    build: ./zuul-api-gateway
    ports:
      - 9999:9999
    depends_on:
      - ui
  
  shoe:
    image: deekshithsn/shoe
    ports:
      - 1002:1002
    depends_on:
      - zuul

  offers:
    image: deekshithsn/offer
    ports:
      - 1001:1001
    depends_on:
      - zuul

  cart:
    image: deekshithsn/cart
    ports:
      - 1004:1004
    depends_on:
      - zuul

  wishlist:
    image: deekshithsn/wishlist
#    volumes:
#      - ./wishlist-microservice-python:.
    ports:
      - 1003:5000
    depends_on:
      - zuul
