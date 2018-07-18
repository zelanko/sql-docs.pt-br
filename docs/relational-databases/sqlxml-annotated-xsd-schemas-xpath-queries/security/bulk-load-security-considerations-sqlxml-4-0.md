---
title: Em massa de considerações de segurança de carga (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- bulk load [SQLXML], security
- security [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], security
ms.assetid: 192fc6d4-ecbc-4a4d-a5cb-55e1f64af318
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dd240ede23b5ff4845531bebf24529bd0219c5ed
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37971838"
---
# <a name="bulk-load-security-considerations-sqlxml-40"></a>Considerações sobre segurança de carregamento em massa (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Estas são as diretrizes de segurança para o uso do carregamento em massa XML:  
  
-   Quando você especifica que o carregamento em massa de operação deve ser executado como uma transação, use o **TempFilePath** propriedade para especificar uma pasta na qual criar os arquivos temporários.  
  
     O processo de carregamento em massa cria esses arquivos temporários com as seguintes permissões:  
  
    -   O acesso de leitura/gravação/exclusão é concedido ao processo de carregamento em massa.  
  
    -   A permissão de leitura é concedida a todos os usuários, porque a conta na qual o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] acessará esses arquivos é desconhecida. É possível restringir o acesso a esses arquivos temporários, definindo as permissões apropriadas na pasta em que estão contidos.  
  
-   O carregamento em massa XML propriamente dito não tem nenhuma configuração de permissão. Supõe-se que o banco de dados esteja configurado corretamente e que o contexto do usuário (ou seja, o logon em que o carregamento em massa está definido) tenha o conjunto de permissões apropriado.  
  
-   Em modo não transacional, caso ocorra um erro durante o processo de carregamento em massa, os dados podem permanecer em um estado de carregamento parcial. Quando isso acontecer, o carregamento em massa apenas será interrompido no ponto em que parou. O modo transacional pode ser usado para aliviar esse problema.  
  
-   Quando ocorrem erros no carregamento em massa, eles podem incluir informações sobre o banco de dados. Por exemplo, eles podem incluir o nome de uma tabela ou coluna, ou informações do tipo de coluna. Ao usar o carregamento em massa, você deve tomar o cuidado de identificar erros no processo e retornar uma mensagem de erro genérica, e não expor diretamente os erros aos usuários.  
  
-   O carregamento em massa não define nenhum limite quanto à quantidade de dados com a qual funciona. O carregamento em massa não faz nenhuma verificação quanto ao tamanho dos dados a serem carregados. É de responsabilidade do usuário executar o carregamento em massa para garantir que haja memória suficiente para processar o arquivo especificado e que haja espaço o bastante no banco de dados para armazenar os dados carregados.  
  
-   O carregamento em massa não faz nenhuma tentativa de usar os dados fornecidos como código. A entrada de dados jamais é executada de qualquer jeito. Qualquer código ou comando nos dados de entrada é tratado como dados normais e não serão executados.  
  
-   O carregamento em massa pode fazer alterações na formatação dos dados fornecidos com base nas diferenças entre o XML e os modelos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por exemplo, o formato para especificar hora é diferente. O carregamento em massa tentará resolver essas diferenças. Como resultado, algumas informações de precisão podem ser perdidas.  
  
-   O carregamento em massa não define nenhum limite quanto ao tempo necessário ao processamento dos dados. O processamento continuará até ser concluído ou ocorrer um erro.  
  
-   O carregamento em massa pode criar e excluir tabelas temporárias dentro do banco de dados, e precisa de permissões para isso. As permissões nessas tabelas serão dadas ao mesmo usuário que está se conectando ao banco de dados para o processo de carregamento em massa.  
  
-   O carregamento em massa pode criar e excluir arquivos temporários usados durante o processamento em modo transacional, e precisa de permissões para isso. Esses arquivos são criados com as mesmas permissões do usuário atual do thread no qual o carregamento em massa está em execução.  
  
-   Caso o usuário defina um arquivo de log de erros do SQLXML no qual gravar os erros, sempre que o carregamento em massa é executado, o arquivo é substituído com dados do processo de carregamento em massa mais recente.  
  
## <a name="see-also"></a>Consulte também  
 [Executar o carregamento em massa de dados XML &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
