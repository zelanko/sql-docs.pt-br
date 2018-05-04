---
title: Instalando o Gerenciador de Driver (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
caps.latest.revision: 59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e465c3fa67375316be9cfbe614dfd5bfa62b7823
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="installing-the-driver-manager"></a>Instalando o Gerenciador de Driver
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo contém instruções para instalar o Gerenciador de Driver unixODBC para uso com todas as versões do Microsoft ODBC Driver for SQL Server no Linux e macOS.  

> [!IMPORTANT]  
> Exclua qualquer pacote de gerenciador de driver instalado em seu computador antes de instalar o Gerenciador de Driver unixODBC. A instalação do Gerenciador de Driver unixODBC pode causar uma falha em um Gerenciador de Driver existente.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Instalando o Gerenciador de Driver do Microsoft ODBC Driver 13 e 13.1 17
A dependência de Gerenciador de driver é resolvida automaticamente pelo sistema de gerenciamento de pacote quando você instala o Microsoft ODBC Driver 13, 13.1 ou 17 para SQL Server no Linux ou macOS, seguindo as instruções em [instalando o Microsoft ODBC Driver para o SQL Server no Linux ou macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Instalando o Gerenciador de Driver para o Microsoft ODBC Driver 11 for SQL Server  

(Somente Red Hat Linux e SUSE.)

**Usando o Script de instalação**  
  
> [!IMPORTANT]  
> Essas instruções se referem à `msodbcsql-11.0.2270.0.tar.gz`, que é o arquivo de instalação do Red Hat Linux. Se você estiver instalando a visualização para SUSE Linux, o nome do arquivo é `msodbcsql-11.0.2260.0.tar.gz`.  

Para instalar o gerenciador de driver:  
  
1.  Verifique se você tem permissão de raiz.  
  
2.  Vá para o diretório onde o [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] download do Driver ODBC colocou o arquivo chamado `msodbcsql-11.0.2270.0.tar.gz`. Verifique se você tem o arquivo \*.tar.gz que corresponde à sua versão do Linux. Para extrair os arquivos, execute o seguinte comando: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  

3.  Altere para o `msodbcsql-11.0.2270.0` diretório e ali, você deverá ver um arquivo chamado `build_dm.sh`. Você pode executar `build_dm.sh` para instalar o Gerenciador de Driver unixODBC.

4.  Para ver uma lista das opções disponíveis, execute o seguinte comando: **./build_dm.sh – ajuda**.  
  
5.  Quando você estiver pronto para instalar, e se o computador pode acessar um site externo por meio de FTP, execute o seguinte comando: **./build_dm.sh**.

Se o computador não pode acessar um site externo por meio de FTP, obtenha `unixODBC-2.3.0.tar.gz`. Você pode obter `unixODBC-2.3.0.tar.gz` de [ http://www.unixodbc.org ](http://www.unixodbc.org/). Clique o **baixar** link no lado esquerdo da página para ir para a página de download. Em seguida, clique no link apropriado para baixar o unixODBC-2.3.0 (não o unixODBC-2.3.1). UnixODBC-2.3.1 não é compatível com esta versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Execute o seguinte comando para iniciar a instalação do Gerenciador de Driver unixODBC: **./build_dm.sh – url de download = file://unixODBC-2.3.0.tar.gz**.  

6.  Tipo **Sim** para prosseguir com a descompactação dos arquivos. Esta parte do processo pode levar até cinco minutos para ser concluída.  

7.  Depois que o script terminar a execução, siga as instruções na tela para instalar o gerenciador do driver unixODBC.

Agora você pode instalar o driver. Para obter mais informações, consulte [instalando o Microsoft ODBC Driver for SQL Server no Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  

**Instalação manual**

Se não for possível concluir o script de instalação, configure e compile o gerenciador de driver correto por conta própria.

1.  Remova qualquer versão mais antiga do unixODBC instalada (por exemplo, unixODBC 2.2.11). No Red Hat Enterprise Linux 5 ou 6, execute o seguinte comando: **yum remover unixODBC**. No SUSE Linux Enterprise, **zypper remover unixODBC**.  
  
2.  Vá para [ http://www.unixodbc.org ](http://www.unixodbc.org/). Clique o **baixar** link no lado esquerdo da página para ir para a página de download. Em seguida, clique no link apropriado para salvar o arquivo unixODBC-2.3.0.tar.gz no seu computador. UnixODBC-2.3.1 não é compatível com esta versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
3.  No seu computador Linux, execute o comando: **tar xvzf unixodbc-2.3.0.tar.gz**.  
  
4.  Altere para o diretório unixODBC-2.3.0.  
  
5.  Em um prompt de comando, execute o comando: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"**.  
  
6.  Em um prompt de comando, execute o comando: **exportar CPPFLAGS**.  
  
7.  Em um prompt de comando, execute o comando: **". / Configurar – = / usr – libdir = / usr/lib64 - sysconfdir = / etc. – Habilitar gui do prefixo = não-- habilitar drivers = não-- enable-iconv-com-iconv-char-enc = UTF8 - com-iconv-uCódigo-enc = UTF16LE"**.  
  
8.  Em um prompt de comando (conectado como raiz), execute o comando: **fazer**.  
  
9. Em um prompt de comando (conectado como raiz), execute o comando: **fazer instalar**.  

Agora você pode instalar o driver. Para obter mais informações, consulte [instalando o Microsoft ODBC Driver for SQL Server no Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  
  
## <a name="see-also"></a>Consulte também
[Instalando o Microsoft ODBC Driver for SQL Server no Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)
