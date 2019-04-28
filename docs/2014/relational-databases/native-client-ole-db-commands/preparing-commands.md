---
title: Preparando comandos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, commands
- prepared statements [SQL Server Native Client]
- commands [OLE DB]
- command preparation [SQL Server Native Client]
ms.assetid: 09ec0c6c-0a44-4766-b9b7-5092f676ee54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9dada733f7729d534b66777f747560cd45530727
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62865014"
---
# <a name="preparing-commands"></a>Preparando comandos
  O provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte à preparação de comando tendo em vista várias execuções de um único comando. No entanto, ela gera sobrecarga, e um cliente não precisa preparar um comando para ser executado mais de uma vez. Em geral, um comando deverá ser preparado se for executado mais de três vezes.  
  
 Por razões de desempenho, a preparação é adiada até que o comando seja executado. Esse é o comportamento padrão. Não são conhecidos erros no comando que está sendo preparada até que ele seja executado ou uma operação de metapropriedade seja executada. Definir a propriedade SSPROP_DEFERPREPARE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como FALSE pode desativar esse comportamento padrão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quando um comando é executado diretamente (sem prepará-lo primeiro), um plano de execução é criado e armazenado em cache. Caso a instrução SQL seja executada novamente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta com um algoritmo eficiente que compara a nova instrução com o plano de execução existente no cache e reutiliza o plano nessa instrução.  
  
 Em comandos preparados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece suporte nativo à preparação e à execução das instruções de comando. Quando você prepara uma instrução, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um plano de execução, o armazena em cache e retorna um identificador desse plano para o provedor. Em seguida, o provedor usa esse identificador para executar a instrução repetidamente. Não é criado nenhum procedimento armazenado. Como o identificador aponta diretamente o plano de execução de uma instrução SQL, e não a correspondência entre a instrução e o plano de execução no cache (como acontece com a execução direta), é mais eficiente preparar uma instrução do que executá-la diretamente, caso você saiba que ela será executada mais de uma vez.  
  
 No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], as instruções preparadas não podem ser usadas para criar objetos temporários e referenciar procedimentos armazenados do sistema que criam objetos temporários, como tabelas temporárias. Esses procedimentos devem ser executados diretamente.  
  
 Alguns comandos jamais devem ser preparados. Por exemplo, os comandos que especificam a execução de procedimento armazenado ou incluem texto tendo em vista a criação do procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jamais devem ser preparados.  
  
 Caso um procedimento armazenado temporário seja criado, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client o executa, retornando resultados como se a instrução propriamente dita fosse executada.  
  
 A criação de procedimento armazenado temporário é controlada pela propriedade de inicialização SSPROP_INIT_USEPROCFORPREP, específica do provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Caso o valor de propriedade seja SSPROPVAL_USEPROCFORPREP_ON ou SSPROPVAL_USEPROCFORPREP_ON_DROP, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client tenta criar um procedimento armazenado durante a preparação de um comando. A criação do procedimento armazenado tem êxito caso o usuário do aplicativo tenha permissões suficientes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para clientes que não costumam se desconectar, a criação de procedimentos armazenados temporários pode exigir recursos significativos de **tempdb**, o banco de dados do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no qual os objetos temporários são criados. Quando o valor SSPROP_INIT_USEPROCFORPREP é SSPROPVAL_USEPROCFORPREP_ ON, os procedimentos armazenados temporários criados pelo provedor de dados OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client só são descartados quando a sessão que criou o comando perde a conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso essa conexão seja a padrão criada na inicialização da fonte de dados, o procedimento armazenado temporário só é descartado quando a fonte de dados deixa de ser inicializada.  
  
 Quando o valor de SSPROP_INIT_USEPROCFORPREP é SSPROPVAL_USEPROCFORPREP_ON_DROP, os procedimentos armazenados temporários do provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client são descartados quando ocorre uma das seguintes condições:  
  
-   O consumidor usa **ICommandText::SetCommandText** para indicar um novo comando.  
  
-   O consumidor usa **ICommandPrepare::Unprepare** para indicar que deixou de exigir o texto de comando.  
  
-   O consumidor libera todas as referências ao objeto de comando que usa o procedimento armazenado temporário.  
  
 Um objeto de comando tem, no máximo, um procedimento armazenado temporário em **tempdb**. Qualquer procedimento armazenado temporário existente representa o texto de comando atual de um objeto de comando específico.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos](commands.md)  
  
  
