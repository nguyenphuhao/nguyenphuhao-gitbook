# Message Queue từ xe bánh tráng trộn

## Lời mở đầu



```typescript
// component.ts
class Component {
  isDone = false;

  handleMessage(order: Message) {
    // Nếu là QUẦY BÁNH TRÁNG
    //    Nhận order tư Order manager
    //    Làm bánh tráng
    // Nếu là KHÁCH HÀNG
    //    Đặt hàng
    // Nếu là ORDER MANAGER
    //    Xử lý order của khách hàng

    this.isDone = true;
  }

  sendMessage(order: Message, recipient: Component) {
    // Gửi bánh tráng đã làm xong cho Order manager
    recipient.handleMessage(message);
  }
}
```

```typescript
// main.ts
const quayBanhTrang1 = new Component();
const quayBanhTrang2 = new Component();
const orderManager = new Component();


//Sau khi nghe điện thoại thì nhận được 2 orders như sau
const orderMesssageABC: OrderMessage = {
  orderId: '100k bánh tráng trộn của chị ABC';
  customerName: 'chị ABC';
  quantity: 10; //10 bịch bánh tráng trộn, mỗi bịch 10k
  product: 'Bánh tráng trộn';
  total: 100_000;
};
const orderMesssageXYZ: OrderMessage = {
  orderId: '50k bánh tráng cuốn của chị XYZ';
  customerName: 'chị XYZ';
  quantity: 10; //10 bịch bánh tráng trộn, mỗi bịch 10k
  product: 'Bánh tráng cuốn';
  total: 50_000;
};

// Tôi nhận order và gửi cho quầy 1
orderManager.sendMessage(orderMesssageABC, quayBanhTrang1);
// Tôi nhận order và gửi cho quầy 2
orderManager.sendMessage(orderMesssageABC, quayBanhTrang2);

function wait(order: OrderMessage){
    //Nếu làm xong bánh rồi thì báo cho order manager biết.
    if (component.isDone) {
        //Order manager giao bánh cho khách hàng
        component.sendMessage(order, orderManager);
        return;
    }
    //Nếu chưa xong thì đợi.
    return wait();
}

wait();
```

Với sự có mặt của **Message Broker** và áp dụng mô hình **Message Driven Programming** vào quy trình trên thì đã mang lại những lợi ích sau

:::info\[Lợi ích khi sử dụng Message Broker]

1. Giảm tải cho Services.
2. Quản lý, điều phối Message và không làm thất thoát Message.
3. Đơn giản hóa quá trình tương tác khi có nhiều Services nữa được tạo ra trong hệ thống. :::

Mô hình hoạt động lúc này không phải là Client-Server nữa mà là

:::tip\[Mô hình Pub-Sub]

1. **Producer** hay gọi tên khác là **Publisher**: Nơi gửi message – Chính là khách hàng mua bánh
2. **Message Broker**: Hệ thống điều hướng message – Chính là tôi
3. **Consumer** hay gọi tên khác là **Subcriber**: Nơi nhận message, thường là những services trong hệ thống – Chính là 2 quầy bánh tráng của mẹ tôi. :::

## Tổng kết

Thông qua câu chuyện trên tôi xin phép tổng hợp lại cho ngắn gọn

**Giai đoạn 1**: Mẹ tôi tương tác, giao dịch trực tiếp với khách hàng. Khách hàng sau phải đợi giao dịch của khách hàng trước xong => Client-Server (Synchronously)

**Giai đoạn 2**: Mẹ tôi nhận order đặt hàng trước qua điện thoại và có thể giao dịch sau với khách hàng => Client-Server (Asynchronously)

**Giai đoạn 3**: Mẹ tôi mở thêm quầy, giao nhiệm vụ xử lý order cho tôi. Tôi đứng giữa làm trung gian điều phối order => Message Driven và tôi là Message Broker.

Thời điểm lúc bấy giờ, tôi vẫn còn cấp sách tới trường nên còn ngồi trực order. Bây giờ, đang ngồi viết bài blog này thì tôi đã là một lập trình viên với 10 năm kinh nghiệm và với công nghệ phát triển vượt bậc như ngày nay thì đã có Message Broker khác thay thế tôi rồi, tôi để lại một vài cái tên để khi bạn cần có thể liên hệ họ. Họ là Grab, Foody, Gojek, ShopeeFood.

Tôi xin phép tạm kết câu chuyện về quầy bánh tráng trộn khởi nghiệp của mẹ tôi tại đây và hẹn gặp lại các bạn trong chuỗi bài viết tiếp theo về RabbitMQ. Trong những bài viết tới, chúng ta sẽ bàn luận nhiều hơn và sâu hơn về RabbitMQ nhé.

```
```
