````
[_webView addObserver:self forKeyPath:@"URL" options:NSKeyValueObservingOptionNew context:nil];

-(void)observeValueForKeyPath:(NSString*)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void*)context{

    NSLog(@"url == %@",self.webView.URL.absoluteString);
}
````
