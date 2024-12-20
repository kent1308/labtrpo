using System;
using System.Drawing;
using System.Windows.Forms;

namespace CinemaSystemUI
{
    public partial class MainWindow : Form
    {
        private Panel mainPanel;
        private Panel moviesPanel;
        private Panel sessionsPanel;
        private Panel contactsPanel;

        public MainWindow()
        {
            InitializeComponent();
        }

        private void InitializeComponent()
        {
            // Основные параметры окна
            this.Text = "Кинотеатр - Главная";
            this.Size = new Size(1024, 768);
            this.StartPosition = FormStartPosition.CenterScreen;
            this.BackColor = Color.White;

            // Верхняя панель навигации
            var topPanel = new Panel
            {
                Dock = DockStyle.Top,
                Height = 60,
                BackColor = Color.DarkSlateGray
            };
            this.Controls.Add(topPanel);

            // Логотип
            var logo = new Label
            {
                Text = "Главная страница", // Убрано слово "Кинотеатр"
                Font = new Font("Arial", 16, FontStyle.Bold),
                ForeColor = Color.White,
                Location = new Point(10, 15)
            };
            topPanel.Controls.Add(logo);

            // Основные разделы
            var navButtons = new[] { "Главная", "Фильмы", "Сеансы", "Контакты" };
            int buttonX = 150;
            foreach (var text in navButtons)
            {
                var navButton = new Button
                {
                    Text = text,
                    Font = new Font("Arial", 10, FontStyle.Bold),
                    ForeColor = Color.White,
                    BackColor = Color.Teal,
                    FlatStyle = FlatStyle.Flat,
                    Location = new Point(buttonX, 15),
                    Size = new Size(100, 30),
                    Tag = text // Используем Tag для определения, какая кнопка была нажата
                };
                navButton.FlatAppearance.BorderSize = 0;
                navButton.Click += NavButton_Click; // Привязываем обработчик клика
                topPanel.Controls.Add(navButton);
                buttonX += 110;
            }

            // Главная панель (основная)
            mainPanel = new Panel
            {
                Dock = DockStyle.Fill,
                BackColor = Color.White
            };
            this.Controls.Add(mainPanel);

            // Создаем остальные панели
            moviesPanel = CreateMoviesPanel();
            sessionsPanel = CreateSessionsPanel();
            contactsPanel = CreateContactsPanel();

            // Показать главную панель по умолчанию
            ShowPanel(mainPanel);
        }

        private void NavButton_Click(object sender, EventArgs e)
        {
            var button = sender as Button;
            if (button == null) return;

            // Определяем, какую панель показывать в зависимости от нажатой кнопки
            switch (button.Tag.ToString())
            {
                case "Главная":
                    ShowPanel(mainPanel);
                    break;
                case "Фильмы":
                    ShowPanel(moviesPanel);
                    break;
                case "Сеансы":
                    ShowPanel(sessionsPanel);
                    break;
                case "Контакты":
                    ShowPanel(contactsPanel);
                    break;
            }
        }

        private Panel CreateMainPanel()
        {
            var panel = new Panel
            {
                Dock = DockStyle.Fill,
                BackColor = Color.White
            };

            var label = new Label
            {
                Text = "Новости кино",
                Font = new Font("Arial", 16, FontStyle.Bold),
                ForeColor = Color.Black,
                Dock = DockStyle.Top,
                TextAlign = ContentAlignment.MiddleCenter
            };
            panel.Controls.Add(label);

            var newsLabel = new Label
            {
                Text = "1. Новый фильм «Невероятные приключения» выходит в прокат в следующем месяце.\n" +
                       "2. Сборы фильма «Оскар 2024» достигли рекорда в 2 млрд долларов.\n" +
                       "3. В Москве пройдет премьера нового блокбастера 'Звездный герой'.",
                Font = new Font("Arial", 12, FontStyle.Regular),
                ForeColor = Color.Black,
                Location = new Point(20, 60),
                Size = new Size(960, 100),
                TextAlign = ContentAlignment.TopLeft
            };
            panel.Controls.Add(newsLabel);

            return panel;
        }

        private Panel CreateMoviesPanel()
        {
            var panel = new Panel
            {
                Dock = DockStyle.Fill,
                BackColor = Color.LightBlue
            };

            var label = new Label
            {
                Text = "Список фильмов",
                Font = new Font("Arial", 16, FontStyle.Bold),
                ForeColor = Color.Black,
                Dock = DockStyle.Top,
                TextAlign = ContentAlignment.MiddleCenter
            };
            panel.Controls.Add(label);

            // Добавим фильмы
            var movieLabel = new Label
            {
                Text = "1. Фильм: 'Секреты вселенной'\n" +
                       "Рейтинг: 8.7/10\n" +
                       "Постер: (Изображение фильма будет здесь)\n\n" +
                       "2. Фильм: 'В поисках приключений'\n" +
                       "Рейтинг: 7.9/10\n" +
                       "Постер: (Изображение фильма будет здесь)",
                Font = new Font("Arial", 12, FontStyle.Regular),
                ForeColor = Color.Black,
                Location = new Point(20, 60),
                Size = new Size(960, 150),
                TextAlign = ContentAlignment.TopLeft
            };
            panel.Controls.Add(movieLabel);

            return panel;
        }

        private Panel CreateSessionsPanel()
        {
            var panel = new Panel
            {
                Dock = DockStyle.Fill,
                BackColor = Color.LightGreen
            };

            var label = new Label
            {
                Text = "Расписание сеансов",
                Font = new Font("Arial", 16, FontStyle.Bold),
                ForeColor = Color.Black,
                Dock = DockStyle.Top,
                TextAlign = ContentAlignment.MiddleCenter
            };
            panel.Controls.Add(label);

            var sessionsLabel = new Label
            {
                Text = "1. 'Секреты вселенной' — 10:00, 13:00, 16:00, 19:00\n" +
                       "2. 'В поисках приключений' — 11:00, 14:00, 17:00, 20:00\n" +
                       "3. 'Звездный герой' — 12:00, 15:00, 18:00, 21:00",
                Font = new Font("Arial", 12, FontStyle.Regular),
                ForeColor = Color.Black,
                Location = new Point(20, 60),
                Size = new Size(960, 100),
                TextAlign = ContentAlignment.TopLeft
            };
            panel.Controls.Add(sessionsLabel);

            return panel;
        }

        private Panel CreateContactsPanel()
        {
            var panel = new Panel
            {
                Dock = DockStyle.Fill,
                BackColor = Color.LightCoral
            };

            var label = new Label
            {
                Text = "Контакты и адреса",
                Font = new Font("Arial", 16, FontStyle.Bold),
                ForeColor = Color.Black,
                Dock = DockStyle.Top,
                TextAlign = ContentAlignment.MiddleCenter
            };
            panel.Controls.Add(label);

            var contactInfo = new Label
            {
                Text = "Телефон: +7 (800) 555-35-35\n" +
                       "Электронная почта: cinema@mail.ru\n" +
                       "Адрес: Москва, ул. Кинотеатрная, д. 12, Россия",
                Font = new Font("Arial", 12, FontStyle.Regular),
                ForeColor = Color.Black,
                Location = new Point(20, 60),
                Size = new Size(960, 100),
                TextAlign = ContentAlignment.TopLeft
            };
            panel.Controls.Add(contactInfo);

            return panel;
        }

        private void ShowPanel(Panel panel)
        {
            // Скрыть все панели
            mainPanel.Visible = false;
            moviesPanel.Visible = false;
            sessionsPanel.Visible = false;
            contactsPanel.Visible = false;

            // Показать нужную панель
            panel.Visible = true;

            // Убедиться, что нужная панель добавлена в Controls (если удалена)
            if (!this.Controls.Contains(panel))
            {
                this.Controls.Add(panel);
            }
        }
    }

    internal static class Program
    {
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new MainWindow());
        }
    }
}
