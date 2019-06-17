---
title: Fontes de dados de arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 733b958ee883aa62034b4acc1eec67100b35a74d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628449"
---
# <a name="file-data-sources"></a>Fontes de dados do arquivo
*Fontes de dados de arquivo* são armazenadas em um arquivo e permitem que as informações de conexão a ser usado repetidamente por um único usuário ou compartilhados entre vários usuários. Quando uma fonte de dados do arquivo é usada, o Gerenciador de Driver faz a conexão à fonte de dados usando as informações em um arquivo. DSN. Esse arquivo pode ser manipulado como qualquer outro arquivo. Uma fonte de dados de arquivo não tem um nome de fonte de dados, como faz uma fonte de dados de máquina e não está registrado para qualquer um usuário ou computador.  
  
 Uma fonte de dados de arquivo simplifica o processo de conexão, porque o arquivo. DSN contém a cadeia de caracteres de conexão que teria que ser criadas para uma chamada para o **SQLDriverConnect** função. Outra vantagem do arquivo. DSN é que ele pode ser copiado para qualquer máquina, portanto, as fontes de dados idênticos podem ser usadas por muitas máquinas, desde que eles tenham o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser compartilhada por aplicativos. Uma fonte de dados de arquivo podem ser compartilhadas pode ser colocada em uma rede e podem ser usada simultaneamente por vários aplicativos.  
  
 Um arquivo. DSN também pode ser não compartilhável. Um arquivo. DSN não compartilhável reside em um único computador e aponta para uma fonte de dados de máquina. Fontes de dados de arquivos não compartilháveis existem principalmente para permitir que a conversão fácil de fontes de dados do computador para fontes de dados de arquivo para que um aplicativo pode ser criado para funcionar somente com fontes de dados de arquivo. Quando o Gerenciador de Driver é enviado as informações em uma fonte de dados de arquivos não compartilháveis, conecta-se conforme o necessário para a fonte de dados de máquina que o arquivo. DSN aponta para.  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../odbc/reference/develop-app/connecting-using-file-data-sources.md), ou o [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.
