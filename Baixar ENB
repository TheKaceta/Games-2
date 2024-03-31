function Show-DownloadProgress {
    param (
        [string]$FileUrl
    )

    $WebRequest = [System.Net.WebRequest]::Create($FileUrl)
    $WebResponse = $WebRequest.GetResponse()
    $FileSize = $WebResponse.ContentLength
    $ProgressBarWidth = 20

    $WebStream = $WebResponse.GetResponseStream()
    $FileStream = New-Object IO.FileStream ("$env:USERPROFILE\Downloads\downloaded_file.rar"), Create, Write
    $BufferSize = 8192
    $Buffer = New-Object byte[] $BufferSize
    $TotalBytesRead = 0

    do {
        $BytesRead = $WebStream.Read($Buffer, 0, $BufferSize)
        $FileStream.Write($Buffer, 0, $BytesRead)
        $TotalBytesRead += $BytesRead
        $PercentComplete = [math]::Round(($TotalBytesRead / $FileSize) * 100, 2)
        $CompletedWidth = [math]::Round(($PercentComplete / 100) * $ProgressBarWidth)
        $RemainingWidth = $ProgressBarWidth - $CompletedWidth
        $ProgressBar = ('█' * $CompletedWidth) + ('▒' * $RemainingWidth)
        Write-Host "`r$ProgressBar $PercentComplete%" -NoNewline
    } while ($BytesRead -gt 0)

    $WebStream.Close()
    $FileStream.Close()
    Write-Host "`nDownload completed!"
}

# Exemplo de uso
Show-DownloadProgress -FileUrl "https://download2299.mediafire.com/e6vj2erlszqgeiP9OayZGD3yF7gMuss1IkmnJEugF5v3dwwOBcOu0vPGQugSs9JC4C0JDwWcmYtVjA5Uz2V8-abgwTq3dgsfn8X4E2CuqCIULjJqpJufP_7j0eOm9TvSeaL9LB2fIMxLiBqbpaYoud0Cm3LXUrbiVdIQbS01B0XPAg/n83ni66lrk0t74j/DATA+LINDA+V25+COM+ENB.rar"
