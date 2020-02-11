---
title: Gerenciando senhas (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b099d0f9-dd37-4c87-8b6f-ed0177881ea4
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d8886f28a30f264e0357af82724567e42e3bd5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907179"
---
# <a name="managing-passwords-accesstosql"></a>Gerenciando senhas (AccessToSQL)
Esta seção trata da proteção de senhas de banco de dados e do procedimento para importá-las ou exportá-las entre servidores:  
  
1.  Protegendo a senha  
  
2.  Exportando ou importando senha criptografada  
  
## <a name="securing-password"></a>Protegendo a senha  
O SSMA permite que você proteja sua senha de um banco de dados.  
  
Use o procedimento a seguir para implementar uma conexão segura:  
  
Especifique uma senha válida usando um dos três métodos a seguir:  
  
1.  **Texto não criptografado:** Digite a senha do banco de dados no atributo Value do nó ' password '. Ele é encontrado no nó definição do servidor na seção servidor do arquivo de script ou arquivo de conexão do servidor.  
  
    As senhas em texto não criptografado não são seguras. Portanto, você encontrará a seguinte mensagem de aviso na saída do console: *" &lt;servidor Server-&gt; ID da senha é fornecido em formato de texto não seguro, o aplicativo do console do SSMA fornece uma opção para proteger a senha por meio de criptografia, consulte a opção-SecurePassword no arquivo de ajuda do SSMA para obter mais informações".*  
  
    **Senhas criptografadas:** A senha especificada, nesse caso, é armazenada em um formato criptografado no computador local no ProtectedStorage. SSMA.  
  
    -   **Protegendo senhas**  
  
        -   Execute o `SSMAforAccessConsole.exe` com o `-securepassword` e adicione a opção na linha de comando passando a conexão do servidor ou o arquivo de script que contém o nó senha na seção definição do servidor.  
  
        -   No prompt, o usuário será solicitado a inserir a senha do banco de dados e confirmá-la.  
  
            As IDs de definição de servidor e suas senhas criptografadas correspondentes são armazenadas em um arquivo no computador local  
  
            Exemplo 1:
            
                Specify password
                
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add all -s "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml" -v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml"
                
                Enter password for server_id 'XXX_1': xxxxxxx
                
                Re-enter password for server_id 'XXX_1': xxxxxxx  
            
            Exemplo 2:
            
                C:\SSMA\SSMAforAccessConsole.EXE -securepassword -add "source_1,target_1" -c "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml" - v "D:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ VariableValueFileSample.xml" -o
                
                Enter password for server_id 'source_1': xxxxxxx
                
                Re-enter password for server_id 'source_1': xxxxxxx
                
                Enter password for server_id 'target_1': xxxxxxx
                
                Re-enter password for server_id 'target _1': xxxxxxx  
  
    -   **Removendo senhas criptografadas**  
  
        Execute o `SSMAforAccessConsole.exe` com a`-securepassword` opção `-remove` e na linha de comando passando as IDs do servidor, para remover as senhas criptografadas do arquivo de armazenamento protegido presente no computador local.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove all
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -remove "source_1,target_1"  
  
    -   **Listando IDs de servidor cujas senhas são criptografadas**  
  
        Execute o SSMAforAccessConsole. exe com a `-securepassword` opção `-list` e na linha de comando para listar todas as IDs de servidor cujas senhas foram criptografadas.  
  
            C:\SSMA\SSMAforAccessConsole.EXE -securepassword -list  
  
    > [!NOTE]  
    > 1.  A senha em texto não criptografado mencionado no arquivo de conexão de script ou servidor tem precedência sobre a senha criptografada no arquivo protegido.  
    > 2.  Quando não houver nenhuma senha na seção do servidor do arquivo de conexão do servidor ou do arquivo de script ou se não tiver sido protegida no computador local, o console do solicitará que você insira a senha.  
  
## <a name="exporting-or-importing-encrypted-passwords"></a>Exportando ou importando senhas criptografadas  
O aplicativo de console do SSMA permite exportar senhas de banco de dados criptografadas presentes em um arquivo no computador local para um arquivo protegido e vice-versa. Ele ajuda a tornar o computador com senhas criptografadas independente. A funcionalidade de exportação lê a ID do servidor e a senha do armazenamento protegido local e salva as informações em um arquivo criptografado. O usuário é solicitado a inserir a senha para o arquivo protegido. Certifique-se de que a senha inserida tenha um comprimento de 8 caracteres ou mais. Esse arquivo protegido é portável em computadores diferentes. A funcionalidade de importação lê a ID do servidor e as informações de senha do arquivo protegido. O usuário é solicitado a inserir a senha para o arquivo protegido e acrescenta as informações ao armazenamento protegido local.  


    Export password
    
    Enter password for protecting the exported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -export all "machine1passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -e "AccessDB_1_1,Sql_1" "machine2passwords.file"
    
    Enter password for protecting the exported file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  


    Import an encrypted password
    
    Enter password for protecting the imported file
    
    C:\SSMA\SSMAforAccessConsole.EXE -securepassword -import all "machine1passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx
    
    C:\SSMA\SSMAforAccessConsole.EXE -p -i "AccessDB_1,Sql_1" "machine2passwords.file"
    
    Enter password to import the servers from encrypted file: xxxxxxxx
    
    Please confirm password: xxxxxxxx  
  
## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
