# lab3
# DA-in-GameDev-lab3
# РАЗРАБОТКА ИГРОВЫХ СЕРВИСОВ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Фудулей Мария Сергеевна
- ХИ41

Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.


Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.

## Цель работы
Cоздание интерактивного приложения с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.
## Задание 1
## Ход работы:
– 1 Практическая работа «Механизм ловли объектов»

– 2 Практическая работа «Добавляем счетчик»

## Результат выполнения хода работы
### 1) Механизм ловли объектов
Для начала создадим скрипт Case. В нем пропишем код, который будет предоставлять возможность управления корзиной. Он выглядит следующим образом:

    void Update()
    {
        Vector3 mousePos2D = Input.mousePosition;
        mousePos2D.z = -Camera.main.transform.position.z;
        Vector3 mousePos3D = Camera.main.ScreenToWorldPoint(mousePos2D);
        Vector3 pos = this.transform.position;
        pos.x = mousePos3D.x;
        this.transform.position = pos;
    }
    
После написания применем скрипт к префабу Case. Скрипт, приведенный выше, позволяет управлять корзиной при помощи мыши. Из-за такой механики скорость корзины по сути не ограничена, что добавляет в игру дизбаланс, однако мы исправим это на моменте отладки. Затем добавим метод к скрипту, описанному выше, который будет удалять объекты, "пойманные" в корзину:

    private void OnCollisionEnter(Collision coll) {
        GameObject Collided = coll.gameObject;
        if (Collided.tag == "Taddy"){
            Destroy(Collided);
        }
    }
### 2) Добавляем счетчик
Добавим объект Cavas. С его помощью мы будем отображать счет игрока. Зайдем в созданный ранее скрипт Case и добавим туда следующие строки кода:
using TMPro;

    public TextMeshProUGUI scoreGT;

    void Start(){
        GameObject scoreGO = GameObject.Find("Score");
        scoreGT = scoreGO.GetComponent<TextMeshProUGUI>();
        scoreGT.text = "0";
    }
// Также дополним метод "OnCollisionEnter"

    private void OnCollisionEnter(Collision coll) {
        GameObject Collided = coll.gameObject;
        if (Collided.tag == "Taddy"){
            Destroy(Collided);
        }
        int score = int.Parse(scoreGT.text);
        score +=1;
        scoreGT.text = score.ToString();
        
    }
В результате счет будет увеличиваться на 1 за каждое пойманное яйцо.
## Задание 2
## Ход работы:
– 3) Практическая работа «Уменьшение жизни. Добавление текстуры»

– 4) Практическая работа «Прибираемся в папке»

## Результат выполнения хода работы

### 3) Уменьшение жизни. Добавление текстуры
Затем перейдем в ранее созданный скрипт "TyanPicker" и добавим туда следующие строки кода:
using UnityEngine.SceneManagement;
public class TyanPicker : MonoBehaviour
{
   public GameObject heartsPrefab;

   public int numHearts = 3;


  
    public List<GameObject> heartList;
    void Start()
    {
        heartList = new List<GameObject>();

        for (int i = 1; i <= numHearts; i++){
            GameObject tSpawnHearts = Instantiate<GameObject>(heartsPrefab);
            tSpawnHearts.transform.position = new Vector3 (-6.5f+i,5.5f,0);
            tSpawnHearts.transform.localScale = new Vector3(0.2f,0.2f,0.2f);

            heartList.Add(tSpawnHearts);
        }
        
    }

 
    void Update()
    {
        
    }

    public void HearDestoyer(){
        int heartIndex = heartList.Count - 1;
        GameObject tSpawnHearts = heartList[heartIndex];
        heartList.RemoveAt(heartIndex);
        Destroy (tSpawnHearts);

        if(heartList.Count == 0){
            SceneManager.LoadScene("2 lesson");
        }
    }
}

  
    }
    
В результате при промахе мы будем терять 1 сердце. При потере всех сердец сцена будет перезапущена.
### 4) Прибираемся в папке

### 5) Интеграция игровых сервисов в готовое приложение


## Задание 3
## Ход работы:
– 5) Практическая работа «Интеграция игровых сервисов в готовое приложение»
## Результат выполнения хода работы
Скачаем плагин "PluginYG_v0.9.1.unitypackage" и интегрируем его в наш проект.Затем добавляем объект YandexGame на каждую сцену. Затем перенастроим билд под WebGL. Забилдим проект в папку и создадим zip архив, который сможем загрузить на платформу Яндекс.

## Выводы
В результате выполнения лабораторной работы №3 мы создали интерактивное приложение с рейтинговой системой пользователя и интеграция игровых сервисов в готовое приложение.
