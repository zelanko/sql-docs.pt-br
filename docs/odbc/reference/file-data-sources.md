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
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068642"
---
# <a name="file-data-sources"></a>Fontes de dados do arquivo
As *fontes de dados de arquivo* são armazenadas em um arquivo e permitem que as informações de conexão sejam usadas repetidamente por um único usuário ou compartilhadas entre vários usuários. Quando uma fonte de dados de arquivo é usada, o Gerenciador de driver faz a conexão com a fonte de dados usando as informações em um arquivo. DSN. Esse arquivo pode ser manipulado como qualquer outro arquivo. Uma fonte de dados de arquivo não tem um nome de fonte de dados, assim como uma fonte de dados de computador e não está registrada em nenhum usuário ou máquina.  
  
 Uma fonte de dados de arquivo simplifica o processo de conexão, pois o arquivo. DSN contém a cadeia de conexão que, de outra forma, teria de ser criada para uma chamada para a função **SQLDriverConnect** . Outra vantagem do arquivo. DSN é que ele pode ser copiado para qualquer computador, de modo que fontes de dados idênticas possam ser usadas por muitas máquinas, desde que tenham o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser compartilhada por aplicativos. Uma fonte de dados de arquivo compartilhável pode ser colocada em uma rede e usada simultaneamente por vários aplicativos.  
  
 Um arquivo. DSN também pode ser descompartilhável. Um arquivo. DSN não compartilhável reside em um único computador e aponta para uma fonte de dados de computador. As fontes de dados de arquivo não compartilháveis existem principalmente para permitir a conversão fácil de fontes de dados de computador em fontes de dados de arquivo para que um aplicativo possa ser criado para funcionar exclusivamente com fontes de dados de arquivo. Quando o Gerenciador de driver recebe as informações em uma fonte de dados de arquivo não compartilhável, ele se conecta conforme necessário para a fonte de dados do computador para a qual o arquivo. DSN aponta.  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar-se usando fontes de dados de arquivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou a descrição da função [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) .
