1. Refactor the code below so that the children will wrap to the next line when the display width is small for them to fit.

-> Use Wrap instead of Row.

class LongStringWidget extends StatelessWidget {
  const LongStringWidget({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Wrap(children: const [
      Chip(label: Text('I')),
      Chip(label: Text('am')),
      Chip(label: Text('looking')),
      Chip(label: Text('for')),
      Chip(label: Text('a')),
      Chip(label: Text('job')),
      Chip(label: Text('and')),
      Chip(label: Text('I')),
      Chip(label: Text('need')),
      Chip(label: Text('a')),
      Chip(label: Text('job')),
    ]);
  }
}

2. Write a function to call the below mentioned API and parse the data. Make sure the function return an object of News item, which contains News article Title,
   News article Content, Date of News Published, Banner Image of News article. https://inshorts.deta.dev/news?category=all
   
-> 

// Data Model

class NewsRes{
  List<NewsData>? newsList;

  NewsRes({this.newsList});

  NewsRes.fromJson(Map<String, dynamic> json) {
    if (json['data'] != null) {
      newsList = <NewsData>[];
      json['data'].forEach((v) {
        newsList!.add(NewsData.fromJson(v));
      });
    }
  }

}

class NewsData {

  String? title;
  String? content;
  String? date;
  String? imageUrl;

  NewsData({this.title, this.content, this.date, this.imageUrl});

  NewsData.fromJson(Map<String, dynamic> json) {
    title = json['title'] != null ? json['title'].toString() : "";
    content = json['content'] != null ? json['content'].toString() : "";
    date = json['date'] != null ? json['date'].toString() : "";
    imageUrl = json['image_url'] != null ? json['image_url'].toString() : "";

  }

  Map<String, dynamic> toJson() {
    final Map<String, dynamic> data = <String, dynamic>{};
    data['title'] = title;
    data['content'] = content;
    data['date'] = date;
    data['image_url'] = imageUrl;
    return data;
  }
}
  
// Repository
  
class NewsRepo {
  Future<NewsRes> newsListApi() async {
    final response = await ApiProvider().fetchNewsData();
    return NewsRes.fromJson(response);
  }
}
  
// Api Provider
  
Future<dynamic> fetchNewsData() async {
    var responseJson;
    try {
      late IOClient client;
      await _getSecureClient().then((value) => client = value);
      final response = await client.get(
          Uri.parse("https://inshorts.deta.dev/news?category=all"));
      responseJson = _returnResponse(response);
      LogUtils.myLog(msg: "RazorpayVerifyOrderRes: ${response.body}");
    } on SocketException {
      throw FetchDataException('No Internet connection.');
    }
    return responseJson;
}  
   
   
3. Identify the problem in the following code block and correct it.   

-> Used Isolate, It basically run in different thread, not lagging UI. Also, It also uses separate memory chunk.

Future<String> makeLongOperationMethod() async {
    return await compute(longOperationMethod, 1000000000);
}

String longOperationMethod(int countTo) {
  var counting = 0;
  for (var i = 1; i <= countTo; i++) {
    counting = i;
  }
  return '$counting! times I print the value!';
}
