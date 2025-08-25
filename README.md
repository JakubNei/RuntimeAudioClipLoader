This asset is no longer needed, since UNity 2022 you can do the same with [following code:](https://discussions.unity.com/t/dynamically-loading-mp3-files-during-runtime/934935/2)
```
IEnumerator LoadAndPlay(string uri)
{
    using (UnityWebRequest www = UnityWebRequestMultimedia.GetAudioClip(uri, AudioType.MPEG))
    {
        yield return www.SendWebRequest();

        if (www.result == UnityWebRequest.Result.ConnectionError || www.result == UnityWebRequest.Result.ProtocolError)
        {
            Debug.LogError("Error: " + www.error);
        }
        else
        {
            AudioClip clip = DownloadHandlerAudioClip.GetContent(www);
            audioSource.clip = clip;
            audioSource.Play();
        }
    }
}
```
