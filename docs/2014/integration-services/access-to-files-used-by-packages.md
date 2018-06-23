---
title: Acesso aos arquivos usados por pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSIS packages, security
- packages [Integration Services], security
- configuration files [Integration Services]
- checkpoint files
- Integration Services packages, security
- logs [Integration Services], security
- files [Integration Services], security
- SQL Server Integration Services packages, security
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0125f75dc0a62886cabedd0f7752b43c426e5f69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009603"
---
# <a name="access-to-files-used-by-packages"></a>Acesso aos arquivos usados por pacotes
  O nível de proteção do pacote não protege arquivos armazenados fora do pacote. Esses arquivos incluem o seguinte:  
  
-   Arquivos de configuração  
  
-   arquivos de ponto de verificação  
  
-   Arquivos de log  
  
 Esses arquivos devem ser protegidos separadamente, especialmente se eles incluírem informações confidenciais.  
  
## <a name="configuration-files"></a>Arquivos de configuração  
 Se você tiver informações confidenciais em uma configuração, como informações de logon e senha, deverá salvar a configuração no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ou usar uma ACL (lista de controle de acesso), para restringir acesso ao local ou à pasta na qual você armazena os arquivos e só permitir o acesso a determinadas contas. Normalmente, você concede acesso às contas que você permite que executem pacotes, e às contas que gerenciam e solucionam problemas de pacotes, que podem incluir revisão do conteúdo de configuração, ponto de verificação e arquivos de log. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece o armazenamento mais seguro porque oferece proteção nos níveis de servidor e de banco de dados. Para salvar configurações no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use o tipo de configuração do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para salvar no sistema de arquivos, use o tipo de configuração XML.  
  
 Para obter mais informações, consulte [Configurações de pacote](../../2014/integration-services/package-configurations.md), [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md)e [Considerações de segurança para uma instalação do SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
## <a name="checkpoint-files"></a>arquivos de ponto de verificação  
 Do mesmo modo, se o arquivo de ponto de verificação usado pelo pacote incluir informações confidenciais, você deverá usar uma lista de controle de acesso (ACL) para proteger o local ou a pasta onde armazena o arquivo. Arquivos de ponto de verificação salvam informações do estado atual no andamento do pacote, bem como os valores atuais das variáveis. Por exemplo, o pacote pode incluir uma variável personalizada que contenha um número de telefone. Para saber mais, confira [Reiniciar pacotes por meio de pontos de verificação](packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="log-files"></a>Arquivos de log  
 As entradas de log que são gravadas no sistema de arquivos também devem ser protegidas usando uma lista de controle de acesso (ACL). As entradas de log também podem ser armazenadas em tabelas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e protegidas pela segurança do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . As entradas de logs podem incluir informações confidenciais, por exemplo, se o pacote contiver uma tarefa Executar SQL que cria uma instrução SQL referente a um número de telefone, a entrada de log para a instrução SQL incluirá o número de telefone. A instrução SQL também pode revelar informações particulares sobre nomes de tabelas e colunas nos bancos de dados. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md).  
  
  