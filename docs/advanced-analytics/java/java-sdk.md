---
title: SDK para Java extension - extensões de linguagem do SQL Server
description: Descrição da extensibilidade Microsoft SDK para Java para Microsoft SQL Server de 2019
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c244d67c7f1cd1636fcd2de0b80454c96927b5d7
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65101819"
---
# <a name="microsoft-extensibility-sdk-for-java-for-sql-server"></a>Extensibilidade do Microsoft SDK para Java para o SQL Server

No SQL Server CTP 2.5, você pode implementar um programa Java para o SQL Server usando a extensibilidade do Microsoft SDK para Java. Esta é uma interface para a extensão da linguagem Java que é usada para trocar dados com o SQL Server e para executar o código Java do SQL Server.

> [!Note]
> O SDK no CTP 2.5 é uma grande mudança de CTPs anteriores. Todos os exemplos tinha o trabalho precisará ser atualizado para usar o SDK em vez disso.

Baixe o [extensibilidade do Microsoft SDK para Java para o Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension).

## <a name="implementation-requirements"></a>Requisitos de implementação

A interface SDK define um conjunto de requisitos que devem ser atendidos para o SQL Server para se comunicar com o tempo de execução do Java. Isso significa que você precisa seguir algumas regras de implementação na classe principal. SQL Server, em seguida, pode executar um método específico dos dados de classe e o exchange do Java usando a extensão da linguagem Java.

Para obter um exemplo de como você pode usar o SDK, consulte o [exemplo de ponta a ponta](java-first-sample.md).

## <a name="sdk-classes"></a>Classes do SDK

Esse SDK consiste em três classes.

Usa duas classes abstratas que definem a interface de extensão Java para trocar dados com o SQL Server:

- **AbstractSqlServerExtensionExecutor**
- **AbstractSqlServerExtensionDataset**

A terceira classe é uma classe auxiliar que contém uma implementação de um objeto de conjunto de dados. Esta é uma classe opcional a usar para tornar mais fácil começar a usar. Você pode usar sua própria implementação de tal classe.

- **PrimitiveDataset**

Abaixo segue os detalhes e o código-fonte para cada classe na extensão de linguagem Java para o SQL Server.

## <a name="abstractsqlserverextensionexecutor"></a>AbstractSqlServerExtensionExecutor

Isso é uma classe abstrata que contém a interface usada para executar o código Java pela extensão de linguagem Java para o SQL Server.

Classe principal Java precisa herdar desta classe. Herdam desta classe significa que há determinados métodos na classe que você precisa implementar em sua própria classe.

Para herdar desta classe abstrata, estender com o nome de classe abstrata na declaração da classe:

```java
public class <MyClass> extends AbstractSqlServerExtensionExecutor {}
```

No mínimo, sua classe principal precisa implementar o método execute(...).

### <a name="method-execute"></a>Método execute

O método execute é o método que é chamado a partir do SQL Server através da extensão de linguagem Java, para invocar código Java do SQL Server. Você deve exibir isso como um método de chave que você inclui principal operações que você deseja executar a partir do SQL Server.

Para passar argumentos de método ao Java do SQL Server, use o `@param` parâmetro em sp_execute_external_script. O método **executar** leva seus argumentos dessa forma.

```java
public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params)  {}
```

### <a name="method-init"></a>Método init

O método init é executado após o construtor e antes do método execute. Todas as operações que precisam ser realizadas antes da execute(...) podem ser feitas neste método.

```java
public void init(String sessionId, int taskId, int numtask) {}
```

### <a name="abstractsqlserverextensionexecutor-source-code"></a>Código-fonte AbstractSqlServerExtensionExecutor

Mais detalhes podem ser encontrados abaixo no código-fonte:

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.UnsupportedOperationException;
import java.util.LinkedHashMap;

/**
 * Abstract class containing interface used by the Java extension
 */
public abstract class AbstractSqlServerExtensionExecutor {
    /* Supported versions of the Java extension */
    public final int SQLSERVER_JAVA_LANG_EXTENSION_V1 = 1;

    /* Members used by the extension to determine application specifics */
    protected int executorExtensionVersion;
    protected String executorInputDatasetClassName;
    protected String executorOutputDatasetClassName;

    public AbstractSqlServerExtensionExecutor() { }

    public void init(String sessionId, int taskId, int numTasks) {
        /* Default implementation of init() is no-op */
    }

    public AbstractSqlServerExtensionDataset execute(AbstractSqlServerExtensionDataset input, LinkedHashMap<String, Object> params) {
        throw new UnsupportedOperationException("AbstractSqlServerExtensionExecutor execute() is not implemented");
    }

    public void cleanup() {
        /* Default implementation of cleanup() is no-op */
    }
}
```

### <a name="abstractsqlserverextensiondataset"></a>AbstractSqlServerExtensionDataset

Classe abstrata que contém a interface para lidar com dados de entrada e saídos usados pela extensão de Java.

```java
package com.microsoft.sqlserver.javalangextension;

import java.lang.UnsupportedOperationException;

/**
 * Abstract class containing interface for handling input and output data used by the Java
 * extension.
 */
public class AbstractSqlServerExtensionDataset {
    /**
     * Column metadata interfaces
     */
    public void addColumnMetadata(int columnId, String columnName, int columnType, int precision, int scale) {
        throw new UnsupportedOperationException("addColumnMetadata is not implemented");
    }

    public int getColumnCount() {
        throw new UnsupportedOperationException("getColumnCount is not implemented");
    }

    public String getColumnName(int columnId) {
        throw new UnsupportedOperationException("getColumnName is not implemented");
    }

    public int getColumnPrecision(int columnId) {
        throw new UnsupportedOperationException("getColumnPrecision is not implemented");
    }

    public int getColumnScale(int columnId) {
        throw new UnsupportedOperationException("getColumnScale is not implemented");
    }

    public int getColumnType(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    public boolean[] getColumnNullMap(int columnId) {
        throw new UnsupportedOperationException("getColumnNullMap is not implemented");
    }

    /**
     * Adding column interfaces
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addIntColumn is not implemented");
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addBooleanColumn is not implemented");
    }

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addLongColumn is not implemented");
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addFloatColumn is not implemented");
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addDoubleColumn is not implemented");
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        throw new UnsupportedOperationException("addShortColumn is not implemented");
    }

    public void addStringColumn(int columnId, String[] rows) {
        throw new UnsupportedOperationException("addStringColumn is not implemented");
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        throw new UnsupportedOperationException("addBinaryColumn is not implemented");
    }

    /**
     * Retrieving column interfaces
     */
    public int[] getIntColumn(int columnId) {
        throw new UnsupportedOperationException("getIntColumn is not implemented");
    }

    public long[] getLongColumn(int columnId) {
        throw new UnsupportedOperationException("getLongColumn is not implemented");
    }

    public float[] getFloatColumn(int columnId) {
        throw new UnsupportedOperationException("getFloatColumn is not implemented");
    }

    public short[] getShortColumn(int columnId) {
        throw new UnsupportedOperationException("getShortColumn is not implemented");
    }

    public boolean[] getBooleanColumn(int columnId) {
        throw new UnsupportedOperationException("getBooleanColumn is not implemented");
    }

    public double[] getDoubleColumn(int columnId) {
        throw new UnsupportedOperationException("getDoubleColumn is not implemented");
    }

    public String[] getStringColumn(int columnId) {
        throw new UnsupportedOperationException("getStringColumn is not implemented");
    }

    public byte[][] getBinaryColumn(int columnId) {
        throw new UnsupportedOperationException("getBinaryColumn is not implemented");
    }
}
```

### <a name="primitivedataset"></a>PrimitiveDataset

Essa classe é uma implementação de **AbstractSqlServerExtensionDataset** que armazena tipos simples como matrizes primitivos. Ele é fornecido no SDK simplesmente como uma classe auxiliar que é opcional usar.

Se você não usar essa classe, você precisa implementar sua própria classe que herda de **AbstractSqlServerExtensionDataset**.  

```java
package com.microsoft.sqlserver.javalangextension;

import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionDataset;
import java.lang.IllegalArgumentException;
import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;

/**
 * Implementation of AbstractSqlServerExtensionDataset that stores
 * simple types as primitives arrays
 */
public class PrimitiveDataset extends AbstractSqlServerExtensionDataset {
    Map<Integer, String>  columnNames;
    Map<Integer, Integer> columnTypes;
    Map<Integer, Integer> columnPrecisions;
    Map<Integer, Integer> columnScales;
    Map<Integer, Object>  columns;
    Map<Integer, boolean[]> columnNullMaps;

    public PrimitiveDataset() {
        columnTypes = new HashMap<>();
        columnNames = new HashMap<>();
        columnPrecisions = new HashMap<>();
        columnScales = new HashMap<>();
        columns = new HashMap<>();
        columnNullMaps = new HashMap<>();
    }

    /**
     * Column metadata interfaces. Metadata is stored in a hash map, using the column ID as the key
     */
    public void addColumnMetadata(int columnId, String columnName, int sqlType, int precision, int scale) {
        if (columnTypes.containsKey(columnId))
        {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " already exists");
        }

        columnTypes.put(columnId, sqlType);
        columnNames.put(columnId, columnName);
        columnPrecisions.put(columnId, precision);
        columnScales.put(columnId, scale);
    }

    public int getColumnCount() {
        return columnTypes.size();
    }

    public String getColumnName(int columnId) {
        checkColumnMetadata(columnId);
        return columnNames.get(columnId);
    }

    public int getColumnPrecision(int columnId) {
        checkColumnMetadata(columnId);
        return columnPrecisions.get(columnId).intValue();
    }

    public int getColumnScale(int columnId) {
        checkColumnMetadata(columnId);
        return columnScales.get(columnId).intValue();
    }

    public int getColumnType(int columnId) {
        checkColumnMetadata(columnId);
        return columnTypes.get(columnId).intValue();
    }

    public boolean[] getColumnNullMap(int columnId) {
        checkColumnMetadata(columnId);
        return columnNullMaps.get(columnId);
    }

    /**
     * Adding column data interfaces. Column data is stored in a hash map, using the column ID as the key and
     * an array of the corresponding type representing each row. Primitives cannot be null, thus null values
     * are represented by an additional boolean array containing a flag to indicate if that value is null.
     * A null indicator array indicates that there are no null values in that column.
     */
    public void addIntColumn(int columnId, int[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addBooleanColumn(int columnId, boolean[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    };

    public void addLongColumn(int columnId, long[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addFloatColumn(int columnId, float[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addDoubleColumn(int columnId, double[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addShortColumn(int columnId, short[] rows, boolean[] nullMap) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
        columnNullMaps.put(columnId, nullMap);
    }

    public void addStringColumn(int columnId, String[] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    public void addBinaryColumn(int columnId, byte[][] rows) {
        checkColumnMetadata(columnId);
        columns.put(columnId, rows);
    }

    /**
     * Retreiving column data interfaces. For primitive types, calling getColumnNullMap() for the column ID
     * will return the boolean array indicating null values.
     */
    public int[] getIntColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (int[])columns.get(columnId);
    }

    public long[] getLongColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (long[])columns.get(columnId);
    }

    public float[] getFloatColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (float[])columns.get(columnId);
    }

    public short[] getShortColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (short[])columns.get(columnId);
    }

    public boolean[] getBooleanColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (boolean[])columns.get(columnId);
    }

    public double[] getDoubleColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (double[])columns.get(columnId);
    }

    public String[] getStringColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (String[])columns.get(columnId);
    }

    public byte[][] getBinaryColumn(int columnId) {
        checkColumnMetadata(columnId);
        return (byte[][])columns.get(columnId);
    }

    private void checkColumnMetadata(int columnId)
    {
        if (!columnTypes.containsKey(columnId)) {
            throw new IllegalArgumentException("Metadata for column ID #: " + columnId + " does not exist");
        }
    }
}
```

## <a name="next-steps"></a>Próximas etapas

+ [Exemplo de Java usando o SDK de ponta a ponta](java-first-sample.md)
+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Extensões de Java no SQL Server](extension-java.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)
