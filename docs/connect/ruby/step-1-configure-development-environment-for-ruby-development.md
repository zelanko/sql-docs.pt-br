---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento para desenvolvimento Ruby | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ruby
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d722d1eed21162d5e076f5dfdfc3a2f18787f42e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento em Ruby
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o Driver Ruby para SQL Server.    
  
Observe que o Driver Ruby usa o protocolo TDS, que é habilitado por padrão no SQL Server e banco de dados do SQL Azure.  Nenhuma configuração adicional é necessária.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Baixar o instalador Ruby**  
Se seu computador não tiver Ruby instale-o. Para novos usuários ruby, é recomendável que você use instaladores 2.2 Ruby. Elas fornecem uma linguagem estável e uma lista abrangente de pacotes (gems) que são compatíveis e atualizado. Acesse o [página de download Ruby](http://rubyinstaller.org/downloads/) e baixar o instalador 2.1. x apropriado. Por exemplo, se você estiver usando um computador de 64 bits, baixe o instalador de Ruby 2.1.6 (x64).   
  
2.  **Instalar Ruby**  
Depois que o instalador é baixado, faça o seguinte:  
a. Clique duas vezes no arquivo para iniciar o instalador.  
b. Selecione seu idioma e concordar com os termos.  
c.  Na tela de configurações de instalação, selecione as caixas de seleção ao lado de ambos os executáveis de Ruby adicionar ao seu caminho e associar RB e .rbw arquivos com esta instalação do Ruby.  
  
3.  **Baixar DevKit Ruby**  
Baixe DevKit da página de RubyInstaller  
  
4.  **Instalar DevKit Ruby**  
Depois que o download estiver concluído, faça o seguinte:  
a. Clique duas vezes no arquivo. Você será solicitado where extrair os arquivos.  
b. Clique no botão "..." e selecione "C:\DevKit". Provavelmente, você precisará criá-la pela primeira vez, clicando em "Criar nova pasta".  
c. Clique em "Okey" e "Extraia", para extrair os arquivos.  
  
5. **Abrir cmd.exe**  
  
6. **Inicializar DevKit Ruby**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalar TinyTDS gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abra terminal**  
  
2. **Instalar a versão do Gerenciador de Ruby (rvm) e pré-requisitos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Use rvm para instalar o Ruby**  
Por exemplo, instale a versão 2.3.0 do Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Certifique-se de que a saída do último comando indica que está executando a versão 2.3.0.  
  
4.  **Instalar o FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instalar TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Observe que o Mac OS X já tem Ruby pré-instalado, como o sistema operacional tem uma dependência.    
  
1.  **Abra terminal**  
  
2. **Instalar o Gerenciador de pacotes do Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalar o FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalar TinyTDS gem**  
```  
> gem install tiny_tds  
```

