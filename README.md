# swift_av_audio_background_play


https://www.notion.so/Swift-background-audio-player-77bb33e7e16d4f67a082d0a9b7d327aa


정말 말도안되게 쉬움 

1. Capabilities에서 background mode를 활성화

# AVSession

2. AVSession 만 활성화 시켜주면 됨

        try AVAudioSession.sharedInstance().setCategory(
            AVAudioSession.Category.playback,
            mode: AVAudioSession.Mode.default,
            options: [AVAudioSession.CategoryOptions.mixWithOthers]
        )


        

# 전체 코드 

        //
        //  ViewController.swift
        //  swift_audio_background
        //
        //  Created by shin seunghyun on 2020/04/11.
        //  Copyright © 2020 shin seunghyun. All rights reserved.
        //
        
        import UIKit
        import AVFoundation
    
        class ViewController: UIViewController {
            
            var audioPlayer = AVAudioPlayer()
        
            override func viewDidLoad() {
                super.viewDidLoad()
                
                let sound = Bundle.main.path(forResource: "music", ofType: "mp3")
                
                do {
                    
                    audioPlayer = try AVAudioPlayer(contentsOf: URL(fileURLWithPath: sound!))
                    //category setting, Audio Session을 열어줘야지 background에서 돌릴 수 있다.
                    try AVAudioSession.sharedInstance().setCategory(
                        AVAudioSession.Category.playback,
                        mode: AVAudioSession.Mode.default,
                        options: [AVAudioSession.CategoryOptions.mixWithOthers]
                    )
                    
                } catch {
                    print(error)
                }
                
            }
        
            @IBAction func play(_ sender: UIButton) {
            
                audioPlayer.play()
                
            }
            
            @IBAction func pause(_ sender: UIButton) {
                
                audioPlayer.pause()
                
            }
            
            
        }
