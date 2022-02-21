package application;

import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

import entities.Employee;

public class Program {
	
	public static void main(String[] args) {
		
		List<Employee> list = new ArrayList<>();
		String path = "C:\\Projetos\\out.txt";
		
		try (BufferedReader br = new BufferedReader(new FileReader(path))) {
			
			String EmployeeCsv = br.readLine();
			while (EmployeeCsv != null) {
				String[] fields = EmployeeCsv.split(",");
				list.add(new Employee(fields[0], Double.parseDouble(fields[1])));
				EmployeeCsv = br.readLine();
			}
			/*
			 * O metodo .sort do Collections, ele mão é aplicavel para uma lista do tipo Employee, por que? o metodo sort,
			 * ele só pode ordenar a lista de tipo T, se esse T for do tipo Comparable, porem a nossa classe Employee aqui
			 * ela não é um tipo Comparable, pra falar que a nossa classe Employee ela é do tipo Comparable, eu vou ter que
			 * implementar essa interface  comparable aqui: public interface Comparable<T> { int compareTo (T o); }
			 * ela é uma interface essa operação aqui: int compareTo (T o);. Isso significa que se eu quiser que o meu
			 * Employee seja ordenavel pelo meu metodo .sort, eu vou ter que implementar a interface Comparable,
			 * implements Comparable<Employee>, ai eu tenho que emplementar o metodo compareTo. 
			 * e pra que que serve esse metodo compareTo? ele serve para comparar um objeto com outro
			 */
			Collections.sort(list);
			for (Employee emp : list) {
				System.out.println(emp.getName() + ", " + emp.getSalary());
			}
			
		} catch (IOException e) {
			System.out.println("Error: " + e.getMessage());
		}
	}
}

===========================================================================

package entities;

public class Employee implements Comparable<Employee> {

	private String name;
	private Double salary;
	
	public Employee() {
	}

	public Employee(String name, Double salary) {
		this.name = name;
		this.salary = salary;
	}

	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}

	public Double getSalary() {
		return salary;
	}
	public void setSalary(Double salary) {
		this.salary = salary;
	}

	/*
	 * eu quero implementar a comparação de um fincionario com outro, ora, quando que um funcionario vai ser menor ou maior
	 * que o outro? o exercicio fala que é pra gente ordenar os funcionarios por nome, então se eu quero comparar um
	 * funcionario com outro baseado no nome, eu posso simplesmente definir que o compareTo de funcionario ele vai
	 * retornar o nome deste funcionario . compareTo(other) funcionario (other.getName()), dessa forma eu ja estou
	 * aproveitando o compareTo da classe String(name), e definindo que a comparação de dois funcionarios é simplesmente
	 * comparar os seus nomes.
	 */
	@Override
	public int compareTo(Employee other) {
		return name.compareTo(other.getName());
		// return salary.compareTo(other.getSalary()); caso eu queira comparar os salarios.
	}
}
