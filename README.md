# HTTPRouter

# Demo

    HTTPRouter srv;

    char text1[] = "GET /uri.cgi HT";
    char text2[] = "TP/1.1\r\nUser-Agent: Mozilla/5.0\r\nAccept: application/json\r\nContent-Length:5\r\n\r\n12345";

    srv.response( [] (HTTPResponse* rep) {
        int len = 0;
        const char * data = rep->bytes( &len );
        printf_s( data );
        delete data;
    } );

    srv.get( "/uri.cgi", []( HTTPRequest* req,HTTPResponse* rep ){
        char data[] = "ABCEDFG\0";
        rep->content( data, sizeof(data) );
        printf( "/uri.cgi callback\r\n" );
    } );


    srv.parse( text1, strlen( text1 ) );
    srv.parse( text2, strlen( text2 ) );
