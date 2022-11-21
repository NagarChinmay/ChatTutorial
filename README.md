# ChatApp

1) Geadle Scripts/build.gradle(app)

2) Geadle Scripts/build.gradle(project)
   
        buildscript {
         
          ext {
                 compose_version = '1.2.1'
                 compose_compiler_version = '1.3.0'
         }
                  
          repositories {
                          google()
                          mavenCentral()
         }
                           
           dependencies {
                          classpath "com.android.tools.build:gradle:7.2.2"
                          classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.7.10"
           }
         }

          task clean(type: Delete) {
                              delete rootProject.buildDir
                            }

4) Layout Activity_main1.xml

5) java/com/example/chat/ui

                    
                    /theme/Color.kt
    
                    /theme/Shape.kt
    
                    /theme/Theme.kt
    
                    /theme/Type.kt
                    
6) java/com/example/chat/ui/MainActivity1

7) java/com/example/chat/ui/MessagesActivity2

# Config

         val offlinePluginFactory = StreamOfflinePluginFactory(
            config = Config(
                backgroundSyncEnabled = true,
                userPresence = true,
                persistenceEnabled = true,
                uploadAttachmentsNetworkType = UploadAttachmentsNetworkType.NOT_ROAMING,
            ),
            appContext = applicationContext,
        )
        
         // 2 - Set up the client for API calls and with the plugin for offline storage
        val client = ChatClient.Builder("ajur4x6b9tjv", applicationContext)
            .withPlugin(offlinePluginFactory)
            .logLevel(ChatLogLevel.ALL) // Set to NOTHING in prod
            .build()
            
             // 3 - Authenticate and connect the user
        val user = User(
            id = "Jalpeshg",
            name = "Jalpeshg",
            )
            
        client.connectUser(
            user = user,
            token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiSmFscGVzaGcifQ.DPXishs_empR7_0lyJtFWivo-oOe9wzPO-EHbFxBaUA"
        ).enqueue()
        
# setOnClick

    btn_click.setOnClickListener {
            startActivity(MessagesActivity2.getIntent(this, "messaging:6377499b571b8751d4aa1df9"))
        }
        
# MessagesActivity[MessagesActivity2 : ComponentActivity()]
   
      override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        // 1 - Load the ID of the selected channel
        val channelId = intent.getStringExtra(KEY_CHANNEL_ID)

        if (channelId == null) {
            finish()
            return
        }

        // 2 - Add the MessagesScreen to your UI
        setContent {
            ChatTheme(
                shapes = StreamShapes
                    .defaultShapes()
                    .copy(
                        avatar = RoundedCornerShape(8.dp),
                        attachment = RoundedCornerShape(16.dp),
                        myMessageBubble = RoundedCornerShape(16.dp),
                        otherMessageBubble = RoundedCornerShape(16.dp),
                        inputField = RectangleShape
                    )
            ) {
                MessagesScreen(
                    channelId = channelId,
                    messageLimit = 30,
                    onBackPressed = { finish() }
                )
            }
        }
    }

    // 3 - Create an intent to start this Activity, with a given channelId
    companion object {
        private const val KEY_CHANNEL_ID = "channelId"

        fun getIntent(context: Context, channelId: String): Intent {
            return Intent(context, MessagesActivity2::class.java).apply {
                putExtra(KEY_CHANNEL_ID, channelId)
            }
        }
      }
