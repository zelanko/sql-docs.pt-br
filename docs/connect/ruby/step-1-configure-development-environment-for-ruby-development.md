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
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992462"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Ruby
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolver um aplicativo usando o driver do Ruby para SQL Server.    
  
Observe que o driver Ruby usa o protocolo TDS, que é habilitado por padrão no SQL Server e no banco de dados SQL do Azure.  Nenhuma configuração adicional é necessária.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Baixar o instalador do Ruby**  
Se seu computador não tiver o Ruby, instale-o. Para novos usuários do Ruby, recomendamos que você use os instaladores do Ruby 2.2. X. Eles fornecem uma linguagem estável e uma extensa lista de pacotes (Gems) que são compatíveis e atualizados. Acesse a [página de download do Ruby](https://rubyinstaller.org/downloads/) e baixe o instalador 2.1. x apropriado. Por exemplo, se você estiver em um computador de 64 bits, baixe o instalador do Ruby 2.1.6 (x64).   
  
2.  **Instalar o Ruby**  
Depois que o instalador for baixado, faça o seguinte:  
A. Clique duas vezes no arquivo para iniciar o instalador.  
B. Selecione seu idioma e concorde com os termos.  
c.  Na tela Configurações de instalação, marque as caixas de seleção ao lado de adicionar executáveis Ruby ao caminho e associar arquivos. rb e. RBW a essa instalação do Ruby.  
  
3.  **Baixar DevKit Ruby**  
Baixar o DevKit da página RubyInstaller  
  
4.  **Instalar o Ruby DevKit**  
Depois que o download for concluído, faça o seguinte:  
A. Clique duas vezes no arquivo. Você receberá uma solicitação para onde extrair os arquivos.  
B. Clique no botão "..." e selecione "C:\DevKit". Você provavelmente precisará criar essa pasta primeiro clicando em "criar nova pasta".  
c. Clique em "OK" e, em seguida, em "extrair", para extrair os arquivos.  
  
5. **Abrir cmd. exe**  
  
6. **Inicializar DevKit Ruby**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instalar o função tinytds Gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abrir terminal**  
  
2. **Instalar o RVM (Ruby version Manager) e os pré-requisitos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Usar o RVM para instalar o Ruby**  
Por exemplo, instale a versão 2.3.0 do Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Verifique se a saída do último comando indica que você está executando a versão 2.3.0.  
  
4.  **Instalar o FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instalar o função tinytds**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
Observe que Mac OS X já tem o Ruby pré-instalado, pois o sistema operacional tem uma dependência.    
  
1.  **Abrir terminal**  
  
2. **Instalar o Gerenciador de pacotes do Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instalar o FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instalar o função tinytds Gem**  
```  
> gem install tiny_tds  
```
