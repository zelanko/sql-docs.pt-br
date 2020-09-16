---
description: Noções básicas sobre níveis de isolamento
title: Noções básicas sobre níveis de isolamento | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 758012112df2bce1b0a7624834bfde3c3c4ece10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488039"
---
# <a name="understanding-isolation-levels"></a>Noções básicas sobre níveis de isolamento

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

As transações especificam um nível de isolamento que define o grau em que uma transação deve ser isolada contra modificações de recursos ou de dados feitas por outras transações. Os níveis de isolamento são descritos em termos de quais efeitos colaterais de simultaneidade são permitidos, como leituras sujas ou leituras fantasma.  
  
Os níveis de isolamento da transação controlam o seguinte:  
  
- Se são feitos bloqueios quando os dados são lidos, e que tipo de bloqueio é solicitado.  
  
- Por quanto tempo os bloqueios de leitura são mantidos.  
  
- Se uma linha de referência de operação de leitura foi modificada por outra transação:  
  
  - É bloqueada até que o bloqueio exclusivo na linha é liberado.  
  
  - Recupera a versão confirmada da linha que existia no momento em que a instrução ou transação foi iniciada.  
  
  - Lê a modificação de dados não confirmada.  

A escolha de um nível de isolamento de transação não afeta os bloqueios adquiridos para proteger as modificações de dados. Uma transação sempre obtém um bloqueio exclusivo em quaisquer dados que ela modifica e mantém esse bloqueio até que a transação seja concluída, seja qual for o nível de isolamento definido para essa transação. Para operações de leitura, níveis de isolamento da transação definem principalmente o nível de proteção dos efeitos das modificações feitas por outras transações.  
  
Um nível de isolamento mais baixo aumenta a capacidade de muitos usuários acessarem os dados ao mesmo tempo, porém aumenta o número de efeitos de simultaneidade, como leituras sujas ou atualizações perdidas, que podem afetar os usuários. Por outro lado, um nível de isolamento mais alto reduz os tipos de efeitos de simultaneidade que os usuários podem encontrar, porém requer mais recursos do sistema e aumenta as chances de uma transação bloquear outra. Escolher o nível de isolamento apropriado depende de equilibrar os requisitos de integridade de dados do aplicativo em relação à sobrecarga de cada nível de isolamento. O nível de isolamento mais alto, serializável, garante que uma transação recuperará exatamente os mesmos dados toda vez que repetir uma operação de leitura, mas faz isto executando um nível de bloqueio que provavelmente causará impacto em outros usuários em sistemas multiusuários. O nível de isolamento mais baixo, leitura não confirmada, pode recuperar dados que foram modificados mas não confirmados por outras transações. Todos os efeitos colaterais da simultaneidade podem ocorrer na leitura não confirmada, mas não há nenhum bloqueio de leitura ou controle de versão, portanto, a sobrecarga é minimizada.  

## <a name="remarks"></a>Comentários

 A tabela a seguir mostra os efeitos colaterais da simultaneidade permitidos pelos diferentes níveis de isolamento.  
  
| Nível de Isolamento  | Leitura suja | Leitura não repetível | Fantasma |
| ---------------- | ---------- | ------------------- | ------- |
| Leitura não confirmada | Sim        | Sim                 | Sim     |
| Leitura confirmada   | Não         | Sim                 | Sim     |
| Leitura repetida  | Não         | Não                  | Sim     |
| Instantâneo         | Não         | Não                  | Não      |
| Serializável     | Não         | Não                  | Não      |
  
As transações devem ser executadas em um nível de isolamento de pelo menos leitura repetível para impedir atualizações perdidas que podem ocorrer quando duas transações recuperam a mesma linha e, em seguida, atualizam a linha com base nos valores originalmente recuperados. Se as duas transações atualizarem as linhas usando uma única instrução UPDATE e não basearem a atualização nos valores previamente recuperados, as atualizações perdidas não poderão ocorrer no nível de isolamento padrão de leitura confirmada.  

Para definir o nível de isolamento de uma transação, você pode usar o método [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Esse método aceita um valor **int** como seu argumento, que tem como base uma das constantes de conexão como no exemplo a seguir:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```

Para usar o novo nível de isolamento de instantâneo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode usar uma das constantes `SQLServerConnection`:  

```java
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```

ou pode usar:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```

Para obter mais informações sobre os níveis de isolamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja "Níveis de isolamento no [!INCLUDE[ssDE](../../includes/ssde_md.md)]" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="see-also"></a>Confira também

[Executando transações com o JDBC Driver](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
