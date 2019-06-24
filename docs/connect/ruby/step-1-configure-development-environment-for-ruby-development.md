---
title: 'Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento de Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ff03ce6ec79aede2e056f0154836e77970af9c50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800819"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Ruby
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o Driver Ruby para SQL Server.    
  
Observe que o Driver Ruby usa o protocolo TDS, que é habilitado por padrão no SQL Server e banco de dados SQL.  Nenhuma configuração adicional é necessária.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Baixe o instalador do Ruby**  
Se seu computador não tiver Ruby instale-o. Para novos usuários do ruby, é recomendável que você use os instaladores de Ruby 2.2. x. Eles fornecem uma linguagem estável e uma lista extensa de pacotes (gems) que são compatíveis e atualizado. Acesse o [página de download Ruby](https://rubyinstaller.org/downloads/) e baixar o instalador apropriado 2.1. x. Para exemplo, se você estiver usando um computador de 64 bits, baixe o instalador do Ruby 2.1.6 (x64).   
  
2.  **Instale o Ruby**  
Depois que o instalador for baixado, faça o seguinte:  
A. Clique duas vezes no arquivo para iniciar o instalador.  
B. Selecione seu idioma e concordar com os termos.  
c.  Na tela de configurações de instalação, marque as caixas de seleção ao lado de ambos os executáveis de adicionar o Ruby para seus arquivos. RB e .rbw caminho e associe-o com esta instalação do Ruby.  
  
3.  **Baixe o Kit de desenvolvimento Ruby**  
Baixe o Kit de desenvolvimento da página RubyInstaller  
  
4.  **Instalar o Kit de desenvolvimento Ruby**  
Depois que o download for concluído, faça o seguinte:  
A. Clique duas vezes no arquivo. Você será solicitado onde extrair os arquivos.  
B. Clique no botão "..." e selecione "C:\DevKit". Provavelmente, você precisará criá-la pela primeira vez, clicando em "Criar nova pasta".  
c. Clique em "Okey" e, em seguida, "extrair," para extrair os arquivos.  
  
5. **Abra cmd.exe**  
  
6. **Inicializar o Kit de desenvolvimento Ruby**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalar a gem TinyTDS**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abrir terminal**  
  
2. **Instalar o Gerenciador de versão do Ruby (rvm) e pré-requisitos**  
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
  
5.  **Instalar o TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Observe que o Mac OS X já tem Ruby pré-instalados, como o sistema operacional tem uma dependência.    
  
1.  **Abrir terminal**  
  
2. **Instalar o Gerenciador de pacotes Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalar o FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalar a gem TinyTDS**  
```  
> gem install tiny_tds  
```
