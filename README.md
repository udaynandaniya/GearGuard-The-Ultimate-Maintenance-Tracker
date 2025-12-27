# GearGuard - The Ultimate Maintenance Tracker

A comprehensive Maintenance Management System built with Django for tracking equipment, managing maintenance teams, and handling repair requests efficiently.

##  Project Overview

GearGuard is a full-featured maintenance management system that helps companies:
- Track equipment and their maintenance history
- Manage maintenance teams and technicians
- Handle both corrective (breakdown) and preventive (scheduled) maintenance
- Visualize workflows using Kanban boards and Calendar views
- Generate reports and analytics

##  Features

### Core Modules

1. **Equipment Module**
   - Track equipment with serial numbers, departments, and locations
   - Monitor purchase dates and warranty information
   - Assign maintenance teams to equipment
   - Track equipment status (Active/Scrapped)

2. **Maintenance Team Module**
   - Create teams (Electrical, Mechanical, IT, etc.)
   - Link technicians to teams
   - Enforce team-based access control

3. **Maintenance Request Module**
   - Two request types: Corrective (Breakdown) and Preventive (Scheduled)
   - Status workflow: New → In Progress → Repaired → Scrap
   - Auto-fill team when equipment is selected
   - Technician assignment and time tracking

4. **Smart Workflows**
   - Auto-fill team from equipment assignment
   - Status transitions with business logic
   - Overdue task highlighting
   - Equipment scrap handling

5. **Visual Management**
   - **Kanban Board**: Drag-and-drop interface for request management
   - **Calendar View**: Visualize preventive maintenance schedules
   - **Dashboard**: Real-time statistics and quick insights

6. **Reporting**
   - Requests per team
   - Equipment maintenance history
   - Corrective vs Preventive ratio
   - Status distribution

## Installation & Setup

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)

### Step 1: Clone or Navigate to Project

```bash
cd "GearGuard_ The Ultimate Maintenance Tracker"
```

### Step 2: Create Virtual Environment (Recommended)

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 5: Create Superuser (Optional)

```bash
python manage.py createsuperuser
```

### Step 6: Load Sample Data

```bash
python manage.py create_sample_data
```

This will create:
- Sample departments (Production, IT, Facilities)
- Maintenance teams (Electrical, Mechanical, IT Support)
- Test users and technicians
- Sample equipment
- Sample maintenance requests

**Test Accounts:**
- Username: `john.electrician` / Password: `password123` (Electrical Team)
- Username: `jane.electrician` / Password: `password123` (Electrical Team)
- Username: `bob.mechanic` / Password: `password123` (Mechanical Team)
- Username: `alice.itsupport` / Password: `password123` (IT Support Team)

### Step 7: Run Development Server

```bash
python manage.py runserver
```

### Step 8: Access the Application

Open your browser and navigate to:
- **Main Application**: http://127.0.0.1:8000/
- **Admin Panel**: http://127.0.0.1:8000/admin/

##  Project Structure

```
GearGuard_ The Ultimate Maintenance Tracker/
├── gearguard/              # Main project configuration
│   ├── settings.py        # Django settings
│   ├── urls.py            # Main URL configuration
│   └── wsgi.py            # WSGI configuration
├── maintenance/           # Main application
│   ├── models.py         # Database models
│   ├── views.py          # View functions
│   ├── forms.py          # Form definitions
│   ├── urls.py           # App URL routing
│   ├── admin.py          # Admin configuration
│   └── management/       # Management commands
│       └── commands/
│           └── create_sample_data.py
├── templates/            # HTML templates
│   ├── base.html        # Base template
│   └── maintenance/     # App templates
├── static/              # Static files (CSS, JS)
├── manage.py           # Django management script
├── requirements.txt    # Python dependencies
└── README.md          # This file
```

##  Business Logic Explained

### Equipment Selection Auto-Fill

When creating a maintenance request:
1. User selects an equipment
2. System automatically fills the assigned team
3. Technician dropdown filters to show only team members

### Request Status Workflow

1. **New**: Request is created, no technician assigned
2. **In Progress**: Technician assigns themselves (only team members can assign)
3. **Repaired**: Technician marks as completed, enters time spent
4. **Scrap**: Equipment is marked as unusable

### Technician Assignment Rules

- Only technicians from the assigned team can work on requests
- When a technician assigns themselves, status automatically changes to "In Progress"
- System validates team membership before allowing assignment

### Overdue Detection

- Requests with scheduled dates in the past are marked as overdue
- Overdue requests are highlighted in red
- Kanban board shows overdue status visually

##  User Interface Features

### Dashboard
- Statistics cards showing key metrics
- Recent maintenance requests
- Quick stats (Corrective vs Preventive ratio)
- Top teams by request count

### Equipment Management
- List view with search and filtering
- Detail view with maintenance history
- "Maintenance (Count)" button linking to related requests
- Equipment status indicators

### Kanban Board
- Drag-and-drop functionality
- Four columns: New, In Progress, Repaired, Scrap
- Technician avatar display
- Overdue task highlighting
- Real-time status updates

### Calendar View
- Monthly calendar layout
- Preventive maintenance visualization
- Click events to view request details
- Upcoming maintenance list

### Reports
- Requests per team with percentages
- Equipment maintenance history (top 10)
- Request type distribution
- Status distribution charts

##  Technical Details

### Database Models

1. **Department**: Company departments
2. **MaintenanceTeam**: Maintenance teams
3. **Technician**: Extended user model with team assignment
4. **Equipment**: Physical equipment with tracking
5. **MaintenanceRequest**: Maintenance requests with workflow

### Key Technologies

- **Django 4.2.7**: Web framework
- **Bootstrap 5**: UI framework
- **jQuery**: JavaScript library
- **SortableJS**: Drag-and-drop functionality
- **SQLite**: Default database (can be changed to PostgreSQL/MySQL)

##  API Endpoints

- `GET /api/equipment-team/`: Get team for selected equipment (for auto-fill)
- `POST /kanban/<id>/update-status/`: Update request status (for drag-and-drop)

##  Customization

### Adding New Departments

1. Go to Admin panel or create via code
2. Departments are used when creating equipment

### Adding New Teams

1. Create via Admin panel or management command
2. Assign technicians to teams
3. Assign teams to equipment

### Customizing Status Workflow

Edit `maintenance/models.py` to modify `STATUS_CHOICES` in `MaintenanceRequest` model.

##  Troubleshooting

### Migration Issues

```bash
python manage.py makemigrations
python manage.py migrate
```

### Static Files Not Loading

```bash
python manage.py collectstatic
```

### Database Reset

```bash
rm db.sqlite3
python manage.py migrate
python manage.py create_sample_data
```

##  Future Enhancements

- Email notifications for overdue tasks
- Mobile app support
- Advanced reporting with charts
- Equipment QR code scanning
- Maintenance history export (PDF/Excel)
- Multi-language support
- Role-based permissions
- Equipment maintenance schedules
- Spare parts inventory management

##  User Roles

Currently, the system supports:
- **Technicians**: Can assign themselves to requests from their team
- **Regular Users**: Can view and create requests
- **Admin**: Full access via Django admin panel

##  License

This project is created for educational and demonstration purposes.

##  Support

For issues or questions:
1. Check the troubleshooting section
2. Review the code comments
3. Check Django documentation

##  Learning Resources

This project demonstrates:
- Django models and relationships
- Form handling and validation
- Business logic implementation
- AJAX requests
- Drag-and-drop interfaces
- Calendar views
- Reporting and analytics

---

**Built with using Django**

