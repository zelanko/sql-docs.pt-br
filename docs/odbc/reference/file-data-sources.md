---
title: Fontes de dados de arquivos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306647"
---
# <a name="file-data-sources"></a>Fontes de dados do arquivo
*As fontes de dados do arquivo* são armazenadas em um arquivo e permitem que as informações de conexão sejam usadas repetidamente por um único usuário ou compartilhadas entre vários usuários. Quando uma fonte de dados de arquivo é usada, o Gerenciador de driver faz a conexão com a fonte de dados usando as informações em um arquivo .dsn. Este arquivo pode ser manipulado como qualquer outro arquivo. Uma fonte de dados de arquivo não tem um nome de origem de dados, assim como uma fonte de dados da máquina, e não está registrada em nenhum usuário ou máquina.  
  
 Uma fonte de dados de arquivo simplifica o processo de conexão, porque o arquivo .dsn contém a seqüência de conexões que, de outra forma, teria que ser construída para uma chamada para a função **SQLDriverConnect.** Outra vantagem do arquivo .dsn é que ele pode ser copiado para qualquer máquina, de modo que fontes de dados idênticas podem ser usadas por muitas máquinas, desde que tenham o driver apropriado instalado. Uma fonte de dados de arquivo também pode ser compartilhada por aplicativos. Uma fonte de dados de arquivo compartilhável pode ser colocada em uma rede e usada simultaneamente por vários aplicativos.  
  
 Um arquivo .dsn também pode ser incompartilhável. Um arquivo .dsn incompartilhável reside em uma única máquina e aponta para uma fonte de dados da máquina. As fontes de dados de arquivos incompartilháveis existem principalmente para permitir a conversão fácil de fontes de dados da máquina para arquivar fontes de dados para que um aplicativo possa ser projetado para funcionar exclusivamente com fontes de dados de arquivos. Quando o Gerenciador de driver é enviado as informações em uma fonte de dados de arquivo não compartilhável, ele se conecta conforme necessário à fonte de dados da máquina que o arquivo .dsn aponta.  
  
 Para obter mais informações sobre fontes de dados de arquivos, consulte [Conectando-se usando fontes de dados de arquivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)ou a descrição da função [SQLDriverConnect.](../../odbc/reference/syntax/sqldriverconnect-function.md)
