This asset is no longer needed, since Unity 2021.3 you can do the same with [following code:](https://discussions.unity.com/t/dynamically-loading-mp3-files-during-runtime/934935/2)
```cs
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
