# Building-a-Todo-List-App-with-React-Native
import React, { useState } from 'react';
import {
  SafeAreaView,
  Text,
  TextInput,
  TouchableOpacity,
  FlatList,
  View,
  StyleSheet,
} from 'react-native';

type Task = {
    id: string;
    title: string;
};

const App = () => {
  const [task, setTask] = useState('');
  const [tasks, setTasks] = useState<{ id: string; title: string }[]>([]);


  const addTask = () => {
    if (task.trim()) {
      setTasks([...tasks, { id: Date.now().toString(), title: task }]);
      setTask('');
    }
  };

  const removeTask = (id : string) => {
    setTasks(tasks.filter((item) => item.id !== id));
  };

  const renderTask = ({ item }: { item: Task }) => (
    <View style={styles.taskContainer}>
      <Text style={styles.taskText}>{item.title}</Text>
      <TouchableOpacity onPress={() => removeTask(item.id)}>
        <Text style={styles.removeText}>X</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Todo App</Text>
      <TextInput
        style={styles.input}
        placeholder="Add a new task..."
        value={task}
        onChangeText={setTask}
      />
      <TouchableOpacity style={styles.addButton} onPress={addTask}>
        <Text style={styles.addButtonText}>Add</Text>
      </TouchableOpacity>
      <FlatList
        data={tasks}
        keyExtractor={(item) => item.id}
        renderItem={renderTask}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f5f5',
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
    textAlign: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 5,
    padding: 10,
    marginBottom: 10,
    fontSize: 16,
  },
  addButton: {
    backgroundColor: '#6200ea',
    padding: 10,
    borderRadius: 5,
    alignItems: 'center',
    marginBottom: 20,
  },
  addButtonText: {
    color: '#fff',
    fontWeight: 'bold',
  },
  taskContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    padding: 10,
    backgroundColor: '#fff',
    borderRadius: 5,
    marginBottom: 10,
    shadowColor: '#000',
    shadowOpacity: 0.1,
    shadowRadius: 5,
    elevation: 2,
  },
  taskText: {
    fontSize: 16,
  },
  removeText: {
    color: '#ff5252',
    fontWeight: 'bold',
    fontSize: 16,
  },
});

export default App;
