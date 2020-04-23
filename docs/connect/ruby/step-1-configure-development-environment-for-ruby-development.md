---
title: 'Etapa 1: configurar o ambiente de desenvolvimento para Ruby'
description: Saiba como configurar o ambiente de desenvolvimento para Ruby.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 700b0c1979b0eccc1544afb59296fba867e24c53
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634589"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>Etapa 1: Configurar o ambiente de desenvolvimento para o desenvolvimento Ruby
Você precisará configurar seu ambiente de desenvolvimento com os pré-requisitos para desenvolvimento um aplicativo usando o Driver do Ruby para SQL Server.    
  
O Driver Ruby usa o protocolo TDS, que é habilitado por padrão no SQL Server e no Banco de Dados SQL do Azure.  É necessário realizar uma configuração adicional.  
  
  
## <a name="windows"></a>Windows  
  
1.  **Baixar o Instalador do Ruby**  
Se o computador não tiver o Ruby, instale-o. Para novos usuários do Ruby, recomendamos o uso dos instaladores do Ruby 2.2.X, que fornecem uma linguagem estável e uma extensa lista de pacotes (gems) compatíveis e atualizados. Acesse a [página de download do Ruby](https://rubyinstaller.org/downloads/) e baixe o instalador 2.1.x apropriado. Por exemplo, se você usa um computador de 64 bits, baixe o instalador do Ruby 2.1.6 (x64).   
  
2.  **Instalar o Ruby**  
Depois de baixar o instalador:  
a. Clique duas vezes no arquivo para iniciar o instalador.  
b. Selecione seu idioma e concorde com os termos.  
c.  Na tela de configurações de instalação, selecione as caixas de seleção ao lado de Adicionar executáveis do Ruby ao seu PATH e de associar arquivos `.rb` e `.rbw` a essa instalação do Ruby.  
  
3.  **Baixar o DevKit do Ruby**  
Baixar o DevKit da página do Instalador do Ruby  
  
4.  **Instalar o DevKit do Ruby**  
Após a conclusão do download:  
a. Clique duas vezes no arquivo. Será solicitado que você forneça um local para a extração dos arquivos.  
b. Clique no botão "..." e selecione "C:\DevKit". Primeiro, você precisará criar essa pasta adequadamente clicando em "Criar Pasta".  
c. Clique em "OK" e depois em "Extrair" para extrair os arquivos.  
  
5. **Abra cmd.exe**  
  
6. **Inicialize o DevKit do Ruby**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **Instale a gem TinyTDS**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Abra o terminal**  
  
2. **Instale o `rvm` (Gerenciador de Versão do Ruby) e os respectivos pré-requisitos**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **Use o `rvm` para instalar o Ruby**  
Por exemplo, instale a versão 2.3.0 do Ruby:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Assegure que a saída do último comando indica que você está executando a versão 2.3.0.  
  
4.  **Instale o FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **Instale o TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="macos"></a>macOS  
  
Observação: o macOS já tem o Ruby pré-instalado, pois o sistema operacional tem uma dependência.
  
1.  **Abra o terminal**  
  
2. **Instale o gerenciador de pacotes do Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **Instale o FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **Instale a gem TinyTDS**  
```  
> gem install tiny_tds  
```
